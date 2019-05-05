<template>
    <div id="app">
        <canvas id="canvas" ref="rendererDOM">
            
        </canvas>
    </div>
</template>

<script>
const THREE = require('THREE');

export default {
    name: 'app',
    data () {
        return {
            msg: 'Welcome to Your Vue.js App',
            SceneVars: {
                scene: null,
                camera: null,
                renderer: null
            },
            window: {
                width: 0,
                height: 0
            },
            obj:{
                cube: null
            }
        }
    },
    mounted() {
        window.addEventListener('resize', this.resizeListener);
        this.resizeListener();
        this.SceneVars.scene = new THREE.Scene();
        this.SceneVars.camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
        this.SceneVars.renderer = new THREE.WebGLRenderer({canvas: this.$refs.rendererDOM, antialias: true});
        this.SceneVars.renderer.setClearColor("#e5e5e5");
        
        this.SceneVars.renderer.setSize(this.window.width, this.window.height);
        var geometry = new THREE.BoxGeometry( 1, 1, 1 );
        var material = new THREE.MeshBasicMaterial( {color: 0x00ff00} );
        this.obj.cube = new THREE.Mesh( geometry, material );
        this.SceneVars.scene.add( this.obj.cube );
        this.SceneVars.camera.position.z = 5;
        this.animate();

    },
    created() {
        
    },
    methods: {
        resizeListener(){
            this.window.width = window.innerWidth;
            this.window.height = window.innerHeight;
        },
        animate(){
            requestAnimationFrame( this.animate );
            this.obj.cube.rotation.x += 0.01;
            this.obj.cube.rotation.y += 0.01;
            this.SceneVars.renderer.render( this.SceneVars.scene, this.SceneVars.camera );
        }
    },
}
</script>

<style lang="scss">

</style>
