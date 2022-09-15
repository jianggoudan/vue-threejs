<template>
<div id="earth"></div>
</template>

<script>
    let scene = null
    let renderer = null
    let camera = null
    let mesh=null
    let mesh2=null
    let controls=null
    let loader=null
    import * as Three from 'three'
    import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
    import {MTLLoader, OBJLoader} from 'three-obj-mtl-loader'    // import {OBJLoader} from 'three/examples/js/loaders/OBJLoader'
    export default {
        data() {
            return {
                publicPath:process.env.BASE_URL
            }
        },
        methods: {
            init(){
                scene = new Three.Scene()
                renderer = new Three.WebGLRenderer();

                loader=new OBJLoader()

                loader.load(`/obj/earth.obj`,(obj)=>{
                    console.log(obj)
                    mesh=obj
                    scene.add(obj);
                })
                var point2 = new Three.PointLight(0xffffff);
                point2.position.set(400, 200, 300); //点光源位置
                scene.add(point2);
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
                setInterval(()=>{
                    this.render()
                },20)

                controls = new OrbitControls(camera,renderer.domElement)
                controls.addEventListener('change',()=>{
                    this.render()
                });
            },
            render() {
                renderer.render(scene, camera);
                mesh.rotateY(0.01)
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

</style>
