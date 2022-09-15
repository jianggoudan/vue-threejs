<!--  -->
<template>

</template>

<script>
    let scene = null
    let renderer = null
    let camera = null
    let mesh = null
    let mesh2 = null
    let controls = null
    import * as Three from 'three'
    import {OrbitControls} from "three/examples/jsm/controls/OrbitControls.js";

    export default {
        data() {
            return {}
        },
        methods: {
            init() {
                scene = new Three.Scene()
                renderer = new Three.WebGLRenderer();

                let geometry1 = new Three.BoxGeometry(100, 100, 300);
                let material1 = new Three.MeshPhongMaterial({
                    color: "black",
                    specular: 0x4488ee,
                    shininess: 12
                });

                mesh = new Three.Mesh(geometry1, material1)
                mesh.position.set(100, 0, 0)
                scene.add(mesh)
                let geometry2 = new Three.SphereGeometry(100, 100, 100);
                let material2 = new Three.MeshLambertMaterial({
                    color: 'black'
                })
                mesh2 = new Three.Mesh(geometry2, material2)
                let mesh3 = mesh2.clone()
                mesh3.translateX(400)
                mesh2.position.set(-150, 0, 0)
                scene.add(mesh2)
                scene.add(mesh3)
                var point2 = new Three.PointLight(0xffffff);
                point2.position.set(400, 200, 300); //点光源位置
                scene.add(point2);
                let point = new Three.PointLight("green");
                point.position.set(800, 0, 0); //点光源位置
                scene.add(point); //点光源添加到场景中
                let ambient = new Three.AmbientLight('white');
                scene.add(ambient);
                // var axisHelper = new Three.AxesHelper(250);
                // scene.add(axisHelper);
                let width = window.innerWidth; //窗口宽度
                let height = window.innerHeight; //窗口高度
                let k = width / height; //窗口宽高比
                let s = 800; //三维场景显示范围控制系数，系数越大，显示的范围越大
                camera = new Three.OrthographicCamera(-s * k, s * k, s, -s, 1, 1000);

                camera.position.set(300, 200, 200); //设置相机位置
                camera.lookAt(scene.position); //设置相机方向(指向的场景对象)

                renderer.setSize(width, height);//设置渲染区域尺寸
                renderer.setClearColor(0xb9d3ff, 1); //设置背景颜色
                document.body.appendChild(renderer.domElement); //body元素中插入canvas对象
                //执行渲染操作   指定场景、相机作为参数
                setInterval(() => {
                    this.render()
                }, 20)

                controls = new OrbitControls(camera, renderer.domElement)
                controls.addEventListener('change', () => {
                    this.render()
                });
            },
            render() {
                renderer.render(scene, camera);
                mesh.rotateY(0.01)
                mesh2.rotateX(0.01)
            },
        },
        mounted() {
            this.init()
        },
        created() {
        },

    }

</script>
<style scoped>
    #container {
        width: 100%;
        height: 100vh;

    }
</style>
