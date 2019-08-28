# ThreeJS-Tutorial
OpenGL  WebGL  Three.js 教程 


# 目录
- [01-WebGL与three.js的基础、与opengl的关系](#01)
- [02-第一个three.js程序](#02)  | [查看Demo](https://ankerleng.github.io/ThreeJS-Tutorial/02-编写第一个three.js程序.html)
- [03-three.js程序框架，绘制一条直线](#03) | [查看Demo](https://ankerleng.github.io/ThreeJS-Tutorial/03-three.js程序框架，绘制一条直线.html)
- gltf 模型展示

<h2 id="01">01-WebGL与three.js的基础、与opengl的关系</h2>

### 什么是WebGL
WebGL 是一项可以在浏览器中流畅展示3D模型和场景的一种技术，他使用JavaScript作为编程语言, 调用浏览器支持的3D绘制函数，来实现3D模型和场景的展现。

### 浏览器为什么能绘制3D世界
因为浏览器实现了OpenGL ES的规范，这套规范可以直接使用指令操作
显卡,使显卡渲染的3D世界,直接反应到浏览器中。

### WebGL能做什么
- 游戏
- 家具
- 虚拟现实
- 城市地图
- CAD制图
- 等等

### WebGL之three.js

Three.js 是一个封装好的webgl库,它使WebGL的学习变得简单

### tree.js的下载
https://threejs.org/

<h2 id="02">02-编写第一个three.js程序</h2> 

### 四大组件：场景
场景就是舞台，你可以把任何要显示的东西，放在场景中的任何位置
```javascript
THREE.SCene = function()
```

那么一个页面是不是只能放一个场景呢？ 答案是否定的，一个页面内可以放多个场景。

### 四大组件：相机
相机就是显示生活的相机，我们最终能够在浏览器中看到的景象就是相机所拍摄的

#### 两大相机
透视相机：透视投影符合人们心理习惯，即离视点近的物体大，离视点远的物体小，远到极点即为消失，成为灭点。

正投影相机：就是远处和近处的物体呈现的是一样大

#### 相机参数
```javascript
THREE.PerspectiveCamera = function(fov,aspect,near,far)
```

### 四大组件：渲染器

渲染器，决定了画家怎么将眼前的场景画到屏幕上渲染即
```javascript
THREE.WebGLRenderer()
```

### 四大组件：几何体
几何体就是要显示在场景中的对象


### 第一个three.js程序
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <title>02-编写第一个three.js程序</title>
    <script src="https://cdn.bootcss.com/three.js/r74/three.js"></script>
</head>

<body>

</body>

<script>
    var scene = new THREE.Scene(); //创建一个场景

    var camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 1, 1000); //创建一个相机

    var renderer = new THREE.WebGLRenderer(); // 创建一个渲染器

    renderer.setClearColor('#ffffff')

    renderer.setSize(window.innerWidth, window.innerHeight);

    document.body.appendChild(renderer.domElement); 

    var geometry = new THREE.CubeGeometry(2, 2, 2);  // 创建一个几何体

    var material = new THREE.MeshBasicMaterial({ color: 0xff0000 }); // 添加一个基础材质， 如果没有材质立方体几乎看不到

    var cube = new THREE.Mesh(geometry, material);  // 网格对象

    scene.add(cube); //将网格加入到场景

    camera.position.z = 5;  // 相机和物体都在坐标原点，什么都看不到，所以将相机移动位置

    function render() {
        requestAnimationFrame(render); // 当浏览器空闲的时候会不断的调用，单线程。 不至于卡死

        cube.rotation.x += 0.01; // 将立方体绕x轴旋转

        cube.rotation.z += 0.01; // 将立方体绕z轴旋转

        cube.rotation.y += 0.01; // 将立方体绕y轴旋转

        renderer.render(scene, camera);  // 通过场景和相机就可以将画面渲染出来
    }

    render();

</script>

</html>
```

<h2 id="03">03-three.js程序框架，绘制一条直线</h2>
