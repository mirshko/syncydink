<template>
  <div id="app">
    <v-touch id="gesture-wrapper" v-on:swiperight="SideNavOpen" v-on:swipeleft="SideNavClose">
      <header>
        <div id="nav-icon" @click="ToggleLeftSidenav">
          <div id="nav-icon3" ref="navicon">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
          </div>
        </div>
        <div ref="hamburgerStartText" id="hamburger-start-text"><md-icon>arrow_back</md-icon> Click/Tap</div>
        <div ref="swipeStartText" id="swipe-start-text"><md-icon>arrow_forward</md-icon> Or Swipe Right</div>
        <div ref="patreonButton" id="patreon-button">
          <!-- I could either let patreon bring in ALL OF FUCKING REACT to render a button, or I could just cut it up and use this. -->
          <div data-reactroot="" class="_2KV-widgets-shared--patreonWidgetWrapper"><a class="sc-bxivhb ffInCX" color="primary" type="button" href="https://www.patreon.com/bePatron?u=2860444&amp;redirect_uri=http%3A%2F%2Fbuttplug.world%2Ftest.html&amp;utm_medium=widget" role="button"><div class="sc-htpNat gdWQYu"><div class="sc-gzVnrw dJCpyC" display="flex" wrap="nowrap" direction="[object Object]"><div class="sc-dnqmqq llsQFn"><span class="sc-htoDjs fqfmvk"><svg viewBox="0 0 569 546" version="1.1" xmlns="http://www.w3.org/2000/svg"><title>Patreon logo</title><g><circle data-color="1" id="Oval" cx="362.589996" cy="204.589996" r="204.589996"></circle><rect data-color="2" id="Rectangle" x="0" y="0" width="100" height="545.799988"></rect></g></svg></span></div><div class="sc-gqjmRU fFOxVX" width="1.5"></div><!-- react-text: 13 -->Give us money<!-- /react-text --></div></div></a></div>
        </div>
      </header>
      <haptic-video-player-component
        v-on:hapticsEvent="onHapticsEvent"
        v-on:hapticsLoaded="onHapticsLoaded"
        v-on:videoPaused="onVideoPaused"
        v-bind:videoMode="this.videoMode"
        v-bind:videoFile="this.videoFile"
        v-bind:hapticsFile="this.hapticsFile" />
      <md-sidenav
        layout="column"
        class="md-left"
        ref="leftSidenav"
        @open="NavIconOpen"
        @close="NavIconClose">
        <md-tabs md-centered>
          <md-tab md-label="Video">
            <md-input-container class="syncydink-nav-file-input">
              <md-file
                accept="video/*"
                placeholder="Click to select video file"
                @selected="onVideoFileChange" />
            </md-input-container>
            <md-input-container class="syncydink-nav-file-input">
              <md-file
                accept="*"
                placeholder="Click to select haptics file"
                @selected="onHapticsFileChange" />
            </md-input-container>
            <div v-if="this.hapticCommandsSize != 0">
              <ul class="haptics-info">
                <li># of Haptic Commands Loaded: {{ this.hapticCommandsSize }}</li>
                <li>Haptics Type: {{ this.hapticCommandsType }}</li>
              </ul>
            </div>
            <div>
              <md-list>
                <md-list-item><md-radio v-model="videoMode" id="video-mode-2d" name="video-mode-group" md-value="2d" class="md-primary" selected>2D</md-radio></md-list-item>
                <md-list-item><md-radio v-model="videoMode" id="video-mode-vr" name="video-mode-group" md-value="split" class="md-primary">2D/VR Split</md-radio></md-list-item>
                <md-list-item><md-radio v-model="videoMode" id="video-mode-vr" name="video-mode-group" md-value="vr" class="md-primary">VR</md-radio></md-list-item>
              </md-list>
            </div>
          </md-tab>
          <md-tab md-label="Buttplug">
            <buttplug-panel-component
              ref="buttplugPanel" />
          </md-tab>
          <md-tab md-label="About">
            <md-list class="md-double-line">
              <md-list-item><b>Syncydink Version 20170829</b></md-list-item>
              <md-list-item><div class="md-list-text-container">Developed By<a href="https://metafetish.com">Metafetish</a></div></md-list-item>
              <md-list-item><div class="md-list-text-container">Need help?<a href="https://metafetish.club/t/tutorial-syncydink-v20170821/82">Tutorial available!</a></div></md-list-item>
              <md-list-item><div class="md-list-text-container">Open Source!<a href="https://github.com/metafetish/syncydink">Code available on Github</a></div></md-list-item>
              <md-list-item><div class="md-list-text-container">We Like Money!<a href="https://patreon.com/qdot">Visit Our Patreon</a></div></md-list-item>
            </md-list>
          </md-tab>
        </md-tabs>
      </md-sidenav>
    </v-touch>
  </div>
</template>

<script lang="ts" src="./App.ts">
</script>

<style src="vue-material/dist/vue-material.css"></style>
<style src="../static/css/video-js.5.4.6.min.css"></style>

<style lang="css">
 @font-face {
   font-family: 'Material Icons';
   font-style: normal;
   font-weight: 400;
   src: local('Material Icons'),
   local('MaterialIcons-Regular'),
   url(../static/fonts/MaterialIcons-Regular.woff2) format('woff2');
 }

 .material-icons {
   font-family: 'Material Icons';
   font-weight: normal;
   font-style: normal;
   font-size: 24px;  /* Preferred icon size */
   display: inline-block;
   line-height: 1;
   text-transform: none;
   letter-spacing: normal;
   word-wrap: normal;
   white-space: nowrap;
   direction: ltr;

   /* Support for all WebKit browsers. */
   -webkit-font-smoothing: antialiased;
   /* Support for Safari and Chrome. */
   text-rendering: optimizeLegibility;

   /* Support for Firefox. */
   -moz-osx-font-smoothing: grayscale;

   /* Support for IE. */
   font-feature-settings: 'liga';
 }

 html, body {
   margin: 0;
   padding: 0;
   height: 100%;
   width:100%
 }

 body {
   background-image:url(../static/images/syncydinklogo.svg);
   background-repeat: no-repeat;
   background-attachment: fixed;
   background-position: center;
 }

 #app {
   height: 100vh;
   width: 100vw;
   font-size: 16px;
   font-weight: 400;
   text-align: left;
   text-transform: none;
   font-family: Roboto,Noto Sans,Noto,sans-serif;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
   color: #2c3e50;
 }

 /* Make our touch wrapper div take up the whole screen, but also make it
    fixed so that we don't have problems with readjustment snapping */
 #gesture-wrapper {
   position: fixed;
   height: 100vh;
   width: 100vw;
 }

 h1, h2 {
   font-weight: normal;
 }

 ul {
   list-style-type: none;
   padding: 0;
 }

 li {
   display: inline-block;
   margin: 0 10px;
 }

 a {
   color: #42b983;
 }

 .md-input-container.md-has-value input {
   font-size:10pt;
 }

 md-sidenav,
 md-sidenav.md-locked-open,
 md-sidenav.md-closed.md-locked-open-add-active {
   min-width: 200px !important;
   width: 85vw !important;
   max-width: 400px !important;
 }

 .md-tabs .md-tab  {
   padding: 0;
 }

 .haptics-info {
   font-size: 14px;
 }

 #hamburger-start-text {
   position: fixed;
   font-size:25px;
   z-index:50;
   top: 33px;
   left: 85px;
 }

 #swipe-start-text {
   position: fixed;
   font-size:25px;
   z-index:50;
   top: 50vh;
   left: 5px;
 }

 /* Taken from https://codepen.io/designcouch/pen/Atyop */

 #nav-icon3 {
   width: 60px;
   height: 45px;
   position: fixed;
   z-index:50;
   top: 20px;
   left: 20px;
   -webkit-transform: rotate(0deg);
   -moz-transform: rotate(0deg);
   -o-transform: rotate(0deg);
   transform: rotate(0deg);
   -webkit-transition: .5s ease-in-out;
   -moz-transition: .5s ease-in-out;
   -o-transition: .5s ease-in-out;
   transition: .5s ease-in-out;
   cursor: pointer;
 }

 #nav-icon3 span {
   display: block;
   position: absolute;
   height: 9px;
   width: 100%;
   background: #3f51b5;
   border-radius: 9px;
   opacity: 1;
   left: 0;
   -webkit-transform: rotate(0deg);
   -moz-transform: rotate(0deg);
   -o-transform: rotate(0deg);
   transform: rotate(0deg);
   -webkit-transition: .25s ease-in-out;
   -moz-transition: .25s ease-in-out;
   -o-transition: .25s ease-in-out;
   transition: .25s ease-in-out;
 }

 /* Icon 3 */

 #nav-icon3 span:nth-child(1) {
   top: 0px;
 }

 #nav-icon3 span:nth-child(2),#nav-icon3 span:nth-child(3) {
   top: 18px;
 }

 #nav-icon3 span:nth-child(4) {
   top: 36px;
 }

 #nav-icon3.open span:nth-child(1) {
   top: 18px;
   width: 0%;
   left: 50%;
 }

 #nav-icon3.open span:nth-child(2) {
   -webkit-transform: rotate(45deg);
   -moz-transform: rotate(45deg);
   -o-transform: rotate(45deg);
   transform: rotate(45deg);
 }

 #nav-icon3.open span:nth-child(3) {
   -webkit-transform: rotate(-45deg);
   -moz-transform: rotate(-45deg);
   -o-transform: rotate(-45deg);
   transform: rotate(-45deg);
 }

 #nav-icon3.open span:nth-child(4) {
   top: 18px;
   width: 0%;
   left: 50%;
 }

 .syncydink-nav-file-input {
   max-width: 95%;
   margin: auto;
 }

 ._2KV-widgets-shared--patreonWidgetWrapper {
   color: #052D49;
   font-family: 'America', 'GT America', 'Lato', 'Helvetica Neue', 'Helvetica', 'Arial', sans-serif;
   font-size: 16px;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
   text-rendering: optimizeLegibility;
 }

 /* Patreon button rendering CSS */

 #patreon-button {
   position: absolute;
   bottom: 0;
   right: 0;
 }

 /* sc-component-id: sc-keyframes-iECmZH */
 @-webkit-keyframes iECmZH{0%{-webkit-transform:rotate(0deg);-ms-transform:rotate(0deg);transform:rotate(0deg);}100%{-webkit-transform:rotate(360deg);-ms-transform:rotate(360deg);transform:rotate(360deg);}}@keyframes iECmZH{0%{-webkit-transform:rotate(0deg);-ms-transform:rotate(0deg);transform:rotate(0deg);}100%{-webkit-transform:rotate(360deg);-ms-transform:rotate(360deg);transform:rotate(360deg);}}
 /* sc-component-id: sc-htpNat */
 .sc-htpNat {}
 .gdWQYu{visibility:visible;}
 /* sc-component-id: sc-bxivhb */
 .sc-bxivhb {}
 .ffInCX{-webkit-backface-visibility:hidden;backface-visibility:hidden;background-color:#F96854;border:2px solid #F96854;border-radius:0;box-sizing:border-box;color:#FFFFFF !important;display:inline-block;font-size:0.8090234857849197rem !important;font-weight:700;padding:0.5rem 0.75rem;position:relative;text-align:center;text-decoration:none;text-transform:uppercase;-webkit-transition:all 300ms cubic-bezier(0.19,1,0.22,1);transition:all 300ms cubic-bezier(0.19,1,0.22,1);-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none;white-space:nowrap;cursor:pointer;}.ffInCX:focus{box-shadow:0 0 8px 0 #358EFF;outline:none;}.ffInCX:hover{background-color:#FA7664;border-color:#FA7664;box-shadow:0 0.25rem 0.75rem rgba(5,45,73,0.09999999999999998);}.ffInCX:active{box-shadow:none;-webkit-transform:translateY(0);-ms-transform:translateY(0);transform:translateY(0);}
 /* sc-component-id: sc-gzVnrw */
 .sc-gzVnrw {}
 .dJCpyC{-webkit-align-content:flex-start;-ms-flex-line-pack:flex-start;align-content:flex-start;-webkit-align-items:center;-webkit-box-align:center;-ms-flex-align:center;align-items:center;display:-webkit-box;display:-webkit-flex;display:-ms-flexbox;display:flex;-webkit-flex-grow:initial;-ms-flex-grow:initial;flex-grow:initial;-webkit-flex-wrap:nowrap;-ms-flex-wrap:nowrap;flex-wrap:nowrap;-webkit-box-pack:center;-webkit-justify-content:center;-ms-flex-pack:center;justify-content:center;styled-components:bug-fix;}@media (min-width:1rem){.dJCpyC{-webkit-flex-direction:row;-ms-flex-direction:row;flex-direction:row;}}
 /* sc-component-id: sc-htoDjs */
 .sc-htoDjs {}
 .fqfmvk{display:-webkit-box;display:-webkit-flex;display:-ms-flexbox;display:flex;}.fqfmvk svg{-webkit-align-self:center;-ms-flex-item-align:center;align-self:center;height:0.75rem;width:0.75rem;}.fqfmvk svg *[data-color='1']{fill:#FFFFFF;-webkit-transition:all 300ms cubic-bezier(0.19,1,0.22,1);transition:all 300ms cubic-bezier(0.19,1,0.22,1);}.fqfmvk svg *[data-color='2']{fill:#052D49;-webkit-transition:all 300ms cubic-bezier(0.19,1,0.22,1);transition:all 300ms cubic-bezier(0.19,1,0.22,1);}
 /* sc-component-id: sc-dnqmqq */
 .sc-dnqmqq {}
 .llsQFn{-webkit-align-self:center;-ms-flex-item-align:center;align-self:center;-webkit-align-items:center;-webkit-box-align:center;-ms-flex-align:center;align-items:center;display:-webkit-inline-box !important;display:-webkit-inline-flex !important;display:-ms-inline-flexbox !important;display:inline-flex !important;padding:NaNrem;}
 /* sc-component-id: sc-gqjmRU */
 .sc-gqjmRU {}
 .fFOxVX{width:0.75rem;height:1px;}

</style>
