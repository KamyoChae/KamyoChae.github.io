threeJs 框架中分 光源 相机 渲染器 几何体 材质 场景 等对象

通过这些对象构建出一个基础的3D场景

构建一个3D场景，需要设置好光源、相机、渲染器和被观测物体

渲染器分3种 
- WebGLRenderer 使用webGL技术 
- CanvasRenderer 使用canvas2D技术
- CSS2DRenderer 和 CSS3Renderer 则是使用CSS技术 
 
 不同渲染器有不同特点 
 简单来说 webgl最为强大 
 另外三种兼容性最好 但存有一定局限性 
 
 ```html
<div id="retina"></div> 
```
 ```javascript
 let renderer // 渲染器 
 let width 
 let height 
 function initRender (){
  width = window.innerWidth 
  height = window.innerHeight 
  renderer = new THREE.Renderer({
    antialias : true 
  })
  renderer.setSize(width, height) // 设置宽高 
  renderer.setClearColor("#000000", 1.0) // 设置背景颜色
  renderer.setPixelRato(window.devicePixelRatio) // 设置像素比 
  document.getElementById("retina").appendChild(renderer.domElement) // 把渲染器放置到页面中 
 }
 
 ```
 
创建相机 
相机的作用相当于人眼 决定了观察的视觉和位置 

