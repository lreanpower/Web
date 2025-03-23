# THREE.JS

three.js文件包

```js
three.js-文件包
└───build——three.js相关库，可以引入到你的.html文件中。
    │
└───docs——Three.js API文档文件
    │───index.html——打开该文件，本地离线方式预览threejs文档
└───examples——大量的3D案例，是你平时开发参考学习的最佳资源
    │───jsm——threejs各种功能扩展库
└───src——Three.js引擎的源码，有兴趣可以阅读。
    │
└───editor——Three.js的可视化编辑器，可以编辑3D场景
    │───index.html——打开应用程序  

```

项目的开放环境引入three

```js
// 比如安装148版本
npm install three@0.148.0 --save
// 引入three.js
import * as THREE from 'three';

// 引入扩展库--新版本OrbitControls.js和GLTFLoader.js
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
// 扩展库引入——旧版本，比如122, 新版本路径addons替换了examples/jsm
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

```

## 1.场景

```js
import * as THREE from 'three';

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
const renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );
```

### 1.1物体

```
BatchedMesh
Bone
Group
InstancedMesh
Line
LineLoop
LineSegments
LOD
Mesh
Points
Skeleton
SkinnedMesh
Sprite
```

#### 1.1.1材质

```
LineBasicMaterial
LineDashedMaterial
Material
MeshBasicMaterial
MeshDepthMaterial
MeshDistanceMaterial
MeshLambertMaterial
MeshMatcapMaterial
MeshNormalMaterial
MeshPhongMaterial
MeshPhysicalMaterial
MeshStandardMaterial
MeshToonMaterial
PointsMaterial
RawShaderMaterial
ShaderMaterial
ShadowMaterial
SpriteMaterial
```

#### 1.1.2几何体

```
BoxGeometry
CapsuleGeometry
CircleGeometry
ConeGeometry
CylinderGeometry
DodecahedronGeometry
EdgesGeometry
ExtrudeGeometry
IcosahedronGeometry
LatheGeometry
OctahedronGeometry
PlaneGeometry
PolyhedronGeometry
RingGeometry
ShapeGeometry
SphereGeometry
TetrahedronGeometry
TorusGeometry
TorusKnotGeometry
TubeGeometry
WireframeGeometry
```



### 灯光和阴影

```html

AmbientLight （环境光）
环境光会均匀的照亮场景中的所有物体,不能投射阴影，因为它没有方向。
RectAreaLight （平面光）
模拟像明亮的窗户或者条状灯光光源，不能投射阴影
HemisphereLight （半球光）
光照颜色从天空光线颜色渐变到地面光线颜色，不能投射阴影

Light
LightProbe

PointLight （点光源）
模拟一个灯泡发出的光，能投射阴影
DirectionalLight（平行光）
模拟太阳光的效果,能投射阴影
SpotLight （聚光灯）
光线从一个点沿一个方向射出，随着光线照射的变远，光线圆锥体的尺寸也逐渐增大，能投射阴影

灯光 / 阴影
LightShadow
PointLightShadow
DirectionalLightShadow
SpotLightShadow
```



## 2.相机

```js
//相机是一个视锥体，有视野角度，长宽比，近裁截面，远裁截面
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
```

透视相机（PerspectiveCamera）用来模拟人眼所看到的景象

正交相机（OrthographicCamera）无论物体距离相机距离远或者近，在最终渲染的图片中物体的大小都保持不变。

立体相机（StereoCamera）用于创建[3D Anaglyph](https://en.wikipedia.org/wiki/Anaglyph_3D)（3D立体影像） 或者[Parallax Barrier](https://en.wikipedia.org/wiki/parallax_barrier)（视差屏障）。

摄像机阵列（ArrayCamera）

立方相机（CubeCamera）

## 3.渲染器

```js

const renderer = new THREE.WebGLRenderer({ antialias:true减少边缘锯齿 });
renderer.setPixelRatio(window.devicePixelRatio);//设置像素比率，避免屏幕模糊
renderer.setSize( window.innerWidth, window.innerHeight );//设置渲染器窗口大小
document.body.appendChild( renderer.domElement );
```

## 4.辅助对象

```
ArrowHelper
AxesHelper
BoxHelper
Box3Helper
CameraHelper
DirectionalLightHelper
GridHelper
PolarGridHelper
HemisphereLightHelper
PlaneHelper
PointLightHelper
SkeletonHelper
SpotLightHelper
```

## 5.核心

```
核心
BufferAttribute
BufferGeometry
Clock
EventDispatcher
GLBufferAttribute
InstancedBufferAttribute
InstancedBufferGeometry
InstancedInterleavedBuffer
InterleavedBuffer
InterleavedBufferAttribute
Layers
Object3D
Raycaster
Uniform
核心 / BufferAttributes
BufferAttribute Types
```

## 6.外部库

### 6.1stats性能监视器（计算渲染帧率FPS）

```js
1.外部显示导入
2.const stats = new Stats();//创建stats对象
  stats.setMode(mode); //mode默认为0，显示渲染帧率，1，显示渲染周期
3.document.body.appendChild(stats.domElement);//stats.domElement:web页面上输出计算结果，一个div元素
4.function reder(){
   //requestAnimationFrame循环调用的函数中调用方法update()，来刷新时间
   stats.update();
   renderer.render(scene,camera);//执行渲染操作
   requestAnimationFrame(render);//请求再次执行渲染函数render，渲染下一帧
}
```

### 6.2GUI库（可视化改变三维场景）

```js
外部显示导入
const gui = new GUI();
const obj={
    x:1,
    color:0x00ffff
}
gui.add(控制对象，对象具体属性，其它参数)
//参数3、参数4数据类型：数字（拖动条）
gui.add(obj,'x',1,180).name('设置x属性别名').step(设置每次改变的属性值间隔).addColor(obj,'color生成颜色值改变的交互界面').onChang(function(value){
   //当obj的x属性变化时，此时obj.x的值=value
   //你可以写任何你想跟着obj.x同步变化的代码
})
//参数3数据类型：数组或对象（选择栏）
gui.add(obj,'scale',[-100,0,100])
gui.add(obj,'scale',{
  //left:-100,
  //center:0,
 // right:100,
  上：-100，
  中：0，
  下：100，
})
//使用.addFolder()创建子菜单
const matFolder=gui.addFolder('子菜单名')
//.open()和.close()方法表示菜单默认展开或收起
```

## 7.设置灯光阴影

```js
1.材质满足能够对光照有反应

2.设置渲染器开启阴影计算  renderer.shadowMap.enabled=true;

3.设置光照阴影投射 directionalLight.castShadow=true;

4.设置物体投射阴影 sphere.castShadow=true;

5.设置物体接收阴影 plane.receiveShadow=ture;
 directionalLight.shadow.radius=20  //阴影贴图边缘模糊度
 directionalLight.shadow.mapSize.width=2048;	// 阴影贴图宽度设置为2048像素
 directionalLight.shadow.mapSize.height=2048;	// 阴影贴图高度设置为2048像素
//directionalLight投射光线类似于一个长方体相机，有二维坐标系平行射向目标，可设置top、bottom等调节阴影贴图大小
 directionalLight.shadow.camera.top = 50; 
 directionalLight.shadow.camera.bottom =-50; 
 directionalLight.shadow.camera.left = -22;
 directionalLight.shadow.camera.right = 22;
//调节投射光线长短和角度
directionalLight.shadow.camera.near = 0.5;
directionalLight.shadow.camera.far = 300;
directionalLight.shadow.camera.fov = 30;

```

## 8.根据浏览器变化自适应画面

```js
//监听画面变化，更新渲染画面
window.addEventListener('resize', () => {
            //更新摄像头
            camera.aspect = window.innerWidth / window.innerHeight;
            //更新摄像机的投影矩阵
            camera.updateProjectionMatrix();
            //更新渲染器
            renderer.setSize(window.innerWidth, window.innerHeight)
            //设置渲染器的像素比
            renderer.setPixelRatio(window.devicePixelRatio)
        })
```

## 9.着色器

### 1.什么是着色器材质

看色器材质(ShaderMaterial)是一个用GLSL编写的小程序，在GPU上运行，它能够提供materials之外的效果，也可以
将许多对象组合成单个Geometry或BufferGeometryl以提高性能

### 2.着色器材质的变量

每个着色器材质都可以指定两种不同类型的shaders,他们是顶点着色器和片元着色器Vertex shaders and fragment

shaders)。

- 顶点着色器首先运行，它接收attributes,计算/操纵每个单独顶点的位置，并将其他数据(varyings)传递给片元着色
  器。

- precision [lowp] float 设置渲染浮点数计算精度是小数点后多少位。（根据自己电脑性能需求设置）

  highp -2^16 - 2^16

  mediump -2^10 - 2^10

  lowp -2^8 - 2^ 2^8

- 片元（或像素）看色器后运行：它设置渲染到屏幕的每个单独的“片元”（像素）的颜色。

  shader中有三种类型的变量uniforms,attributes,和varyings

- Uniforms是所有顶点都具有相同的值的变量，比如灯光，雾，和阴影贴图就是被储存在uniforms中的数据。

  uniforms可以通过顶点着色器和片元着色器来访问。

- Attributes与每个顶点关联的变量。例妆如，顶点位置，法线和顶点颜色都是存储在attributes中的数据。

  attributes只可以在顶点色器中访问。

- Varyings是从顶点看色器传递到片元着色器的变量。对于每一个片元，每一个varying的值将是相邻顶点值的平滑插

  值。

  注意：在shader内部，uniforms和attributes就像常量；你只能使用avaScript代码通过缓冲区来修改它们的值。

### 3.着色器材质的使用

上面说了每个着色器材质都可以指定两种不同类型的shaders,不过如果我们不去指定这两个shadersi而直接使用也不会报
错，因为ShaderMaterial已经定义了默认的顶点看色器和片元看色器，他们的代码是这样的。
