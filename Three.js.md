# [Three.js 入门][1]

标签（空格分隔）： Three.js

---

1.什么是Three.js
-------------
Three.js是一个3D JavaScript库。封装了底层的图形接口，使得程序员可以方便简单的实现三维场景的渲染。

2.起步
----

 - 下载Three.js源码
 - 在html文件中引入Three.js文件
 - 由于WebGL的渲染是需要Canvas元素的。所以创建一个Canvas元素(也可以由Three.js来创建)
 - 在JS代码中定义一个init函数，会在文档加载完成后执行

 一个典型的Three.js程序至少要包括渲染器、场景、照相机，以及在场景中创建的物体。

3.渲染器
-----

渲染器将和canvas元素进行绑定 例如：

    var renderer = new THREE.WebGLRenderer({
        canvas:document.getElementById('main');
    })
上述代码就将渲染器与id为 'main' 的cnavas元素绑定了。当然我们也可以通过Three.js来创建canvas并将其与渲染器进行绑定

    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(400, 300);
    document.getElementsByTagName('body')[0].appendChild(renderer.domElement);
    renderer.setClearColor(0x000000);
上述代码就创建了一个400*400的canvas并将其与渲染器进行了绑定。

4.场景
----

Three.js中所有的物体都是要添加到场景中的，简单使用：

    var scene = new THREE.Scene(); // 实例化一个场景

5.照相机
-----

照相机定义了三维框架到二维屏幕的投影方式,投影方式有正交投影与透视投影,所以照相机又分为正交照相机与透视照相机

1.正交投影照相机

构造函数是:

     THREE.OrthographicCamera(left,right,top,bottom,near,far);

> left/right/top/bottom:左边界，是可视范围的左平面，可被渲染的最左面 near/far:近面/远面，场景渲染的起/止点。

创建一个直透视投影的照相机：

     var camera = new THREE.PerspectiveCamera(45,4/3,1,1000);
     camera.position.set(0,0,5);
     scene.add(camera);  // 将照相机添加到场景中
创建一个长方体：

     var cube = new THREE.Mesh(
         new THREE.CubeGeometry(1,2,3),
         new THREE.MeshBasicMaterial({
             color:0xff0000
         })
     );

2.透视照相机

构造函数是：

     THREE.PerspectiveCamera(fov, aspect, near, far);

> fov:视场，这是从相机位置能看到的部分场景 aspect:渲染结果输出区的横纵方向上的比值

6.基本几何体
-------

 立方体

    THREE.CubeGeometry(width, height, depth, widthSegments,heightSegments, depthSegments);

前3个参数为三个方向上的长度，后三个参数是在三个方向上的分段数。

平面

    THREE.PlaneGeometry(width,height,widthSegments,heightSegments);

球体

    THREE.SphereGeometry(radius, segmentsWidth, segmentsHeight, phiStart, phiLength, the taStart, thetaLength);
radius 是半径； segmentsWidth 表示经度上的切片数； segmentsHeight 表示纬度上的切片数； phiStart 表示经度开始的弧度； phiLength 表示经度跨过的弧度；thetaStart 表示纬度开始的弧度； thetaLength 表示纬度跨过的弧度。

圆形

    THREE.CircleGeometry(radius, segments, thetaStart, thetaLength);
    
圆柱体

    THREE.CylinderGeometry(radiusTop, radiusBottom, height, radiusSegments, heightSegments, openEnded);
    openEnded表示是否有顶面和底面，默认为false，表示有顶面和底面.
    
圆环面

    THREE.TorusGeometry(radius, tube, radialSegments, tubularSegments, arc);
    tube:内部管道半径; arc:圆环面的弧度，默认为2π

圆环结

    THREE.TorusKnotGeometry(radius, tube, radialSegments, tubularSegments, p, q, heightScale);

p和q:控制圆环结的样式; heightScale:在z轴上的缩放。


  [1]: http://ife.baidu.com/note/detail/id/50