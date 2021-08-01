<template>
  <div id="app" class="columns is-marginless">
    <div class="column is-3 has-background-light">
        <aside class="menu">
          <p class="menu-label">General</p>
          <ul class="menu-list">
            <li><router-link to="/">Home</router-link></li>
          </ul>
          <p class="menu-label">PIXI Elements</p>
          <ul class="menu-list">
            <li><router-link to="/renderer">Renderer</router-link></li>
            <li><router-link to="/container">Container</router-link></li>
            <li><router-link to="/sprite">Sprite</router-link></li>
            <li><router-link to="/text">Text</router-link></li>
          </ul>
        </aside>
       
      </div>
    <div id="set">
      <canvas id="myCanvas" width="2122" height="1942" style="touch-action: none  cursor: inherit "></canvas>
      
      
        
     <router-view class="column" />
    </div>
  </div>

</template>

<script>
import * as PIXI from "pixi.js";

// var sc_bottom = left_p + 0
// var scable = 0
// var mx = -1000
// var my = -1000
// var touching = 0
// var scrolling = 0
// var t_touch = 0

function flo() {
  //app
  var ww = window.innerWidth;
  var wh = window.innerHeight;
  var app = new PIXI.Application({
    view: document.getElementById("myCanvas"),
    width: ww,
    height: wh,
    //forceFXAA:true,
    //    preserveDrawingBuffer:true,
    backgroundColor: 0xffffff,
    //    antialias: true,
    resolution: window.devicePixelRatio || 1,
  });
  //app.renderer.autoResize = true
  app.renderer.autoDensity = true;
  app.stage.interactive = true;
  app.cursor = "none";
  app.stage.cursor = "none";
  // window.onresize = sizer
  // window.onload = sizer
  // window.onorientationchange = sizer
  console.log(document.getElementById("set"));
  document.getElementById("set").appendChild(app.view);
}

export default {
  mounted() {
    const canvas = document.createElement("canvas");
    let gl;
    let renderer;
    try {
      gl = canvas.getContext("experimental-webgl");
      const ext = gl.getExtension("WEBGL_debug_renderer_info");
      if (!ext) {
        renderer = "";
      } else {
        renderer = gl.getParameter(ext.UNMASKED_RENDERER_WEBGL);
      }
    } catch (e) {
      gl = null;
      renderer = "";
    }
    flo();
  },
};
</script>

<style lang="css">
#app {
  min-height: 100vh;
}

</style>
