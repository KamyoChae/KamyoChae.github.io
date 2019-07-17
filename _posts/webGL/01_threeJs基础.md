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

THreeJs 提供了多种相机 比较常见的有两种 一种是 PerspectiveCamera 透视投影相机 另一种是OrthographicCamera正交投影相机

其中和人眼观察效果一样的是投影透视相机 

```javascript 
let camera 
let origPoint = new THREE.Vector3(0,0,0)
function initCamera(){
 camera = new THREE.PerspectiveCamera(45, width/ height , 1,1000) // 创建相机
 camera.position.set(200, 400, 600) // 设置相机位置
 camera.up.set(0,1,0) // 设置相机正方向
 camera.lookAt(origPoint) // 设置相机视点 
}

```

 new THREE.PerspectiveCamera(45, width/ height , 1,1000)  参数如下 
 - new THREE.PerspectiveCamera(fov, aspect, near, far)
 - fov表示视角；
 - aspect表示裁切面宽高比；
 - near表示近平面距离；
 - far表示远平面距离；






