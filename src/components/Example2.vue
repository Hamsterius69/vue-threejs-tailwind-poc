<template>
    <div class="text-white absolute mt-2 ml-2">Example 2 - OrbitControls </div>
    <div class="example--box" id="example2"></div>
</template>

<script>
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';
let render = null;
let escena = null;
let camara = null;
let cubo = null;
let cubo1 = null;
let circle = null;
let controls = null;
export default {
    name: 'Example2',
    data() {
		return {
		};
	},
    mounted() {
        this.startEscena();
        this.animarEscena();
        this.renderEscena();
    },
    methods: {
        renderEscena() {
            render.render(escena, camara);
        },
        animarEscena() {
            requestAnimationFrame(this.animarEscena);
            cubo.rotation.y += 0.02; // rotamos el cubo en el eje y 0.02 unidades de medida.
            cubo.rotation.x += 0.02;
            cubo1.rotation.y += 0.02; // rotamos el cubo en el eje y 0.02 unidades de medida.
            cubo1.rotation.x += 0.02;
            circle.rotation.y += 0.02; // rotamos el cubo en el eje y 0.02 unidades de medida.
            circle.rotation.x += 0.02;
            
            controls.update();
            this.renderEscena();
        },
        startEscena() {
            // Render
            render = new THREE.WebGLRenderer(); // definimos el renderizador

            render.setClearColor(0x000000, 1); // el colorde limpieza, negro

            const canvasWidth = 500; // tamaño del canvas
            const canvasHeight = 500; // tamaño del canvas
            render.setSize(canvasWidth, canvasHeight);

            // indicamos que el render pinte la escena en el div canvas
            document.getElementById('example2').appendChild(render.domElement);

            // Escena
            escena = new THREE.Scene(); // definimos la escena
            // escena.fog = new THREE.Fog(0x76456c, 0.1, 8);
            // Camara
            camara = new THREE.PerspectiveCamera(45, canvasWidth / canvasHeight, 0.2, 150);
            camara.position.set(0, 0, 11); // situamos la cámara en las coordenadas absolutas
            camara.lookAt(escena.position); // le indicamos a la cámara que mire la escena.
            //escena.add(camara); // añadimos la cámara a la escena

            // cubo
             const material1 = new THREE.MeshBasicMaterial();
             const material2 = new THREE.MeshBasicMaterial();
             const material3 = new THREE.MeshBasicMaterial();
             material1.color = new THREE.Color('blue');
             material2.color = new THREE.Color('black');
             material3.color = new THREE.Color('white');
             const cuboMateriales = [
                  material1,
                  material2,
                  material3,
              ];
            const cuboGeometria = new THREE.ConeGeometry(0.5, 0.5, 3, 1);

            cubo1 = new THREE.Mesh(cuboGeometria, cuboMateriales);
            cubo1.position.set(0, 0, -3.0);
            //add geometry
            const geometry = new THREE.DodecahedronGeometry(0.7);
            const material = new THREE.MeshBasicMaterial({
              color: 'tomato',
              wireframe: true,
            });
            cubo = new THREE.Mesh(geometry, material);
            cubo.position.z = -3;
            //add geometry
            const geometryC = new THREE.CapsuleGeometry();
            const materialC = new THREE.MeshBasicMaterial({
              color: 'green',
              wireframe: true,
            });
            circle = new THREE.Mesh(geometryC, materialC);
            circle.position.z = -3;
            escena.add(circle);
            escena.add(cubo);
            escena.add(cubo1);

            //control
            controls = new OrbitControls( camara, render.domElement);
            controls.listenToKeyEvents(document.body)
            controls.update();
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.example--box {
    border: solid 2px black;
    width: 500px;
    height: 500px;
}
</style>