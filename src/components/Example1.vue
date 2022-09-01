<template>
  <div class="example--box" id="example1">
  </div>
</template>

<script>
import * as THREE from 'three';
var render = null;
var escena = null;
var camara = null;
var cubo = null;
var cubo1 = null;
var circle = null;
export default {
    name: 'ManageExamples',
    data() {
		return {
            // render: null,
            // escena: null,
            // camara: null,
            // cubo: null,
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
            document.getElementById('example1').appendChild(render.domElement);

            // Escena
            escena = new THREE.Scene(); // definimos la escena
            // escena.fog = new THREE.Fog(0x76456c, 0.1, 8);
            // Camara
            camara = new THREE.PerspectiveCamera(45, canvasWidth / canvasHeight, 0.2, 150);
            camara.position.set(0, 0, 0); // situamos la cámara en las coordenadas absolutas
            camara.lookAt(escena.position); // le indicamos a la cámara que mire la escena.
            escena.add(camara); // añadimos la cámara a la escena

            // cubo
            const material1 = new THREE.MeshBasicMaterial();
            const material2 = new THREE.MeshBasicMaterial();
            const material3 = new THREE.MeshBasicMaterial();
            const material4 = new THREE.MeshBasicMaterial();
            const material5 = new THREE.MeshBasicMaterial();
            const material6 = new THREE.MeshBasicMaterial();
            material1.color = new THREE.Color(0x33FF00);
            material2.color = new THREE.Color(0x00CCFF);
            material3.color = new THREE.Color(0xFF0000);
            material4.color = new THREE.Color(0xFFCC00);
            material5.color = new THREE.Color(0x99FFFF);
            material6.color = new THREE.Color(0xFFFFFF);
            const cuboMateriales = [
                 material1,
                 material2,
                 material3,
                 material4,
                 material5,
                 material6,
             ];
            // const cuboMaterial = new THREE.MeshFaceMaterial(cuboMateriales);
            const cuboGeometria = new THREE.BoxGeometry(1, 1, 1);

            cubo1 = new THREE.Mesh(cuboGeometria, cuboMateriales);
            cubo1.position.set(0, 0, -7.0);
            //add geometry
            const geometry = new THREE.BoxGeometry();
            const material = new THREE.MeshBasicMaterial({
              color: 'tomato',
              wireframe: true,
            });
            cubo = new THREE.Mesh(geometry, material);
            cubo.position.z = -3;
            //add geometry
            const geometryC = new THREE.SphereGeometry();
            const materialC = new THREE.MeshBasicMaterial({
              color: 'green',
              wireframe: true,
            });
            circle = new THREE.Mesh(geometryC, materialC);
            circle.position.z = -3;
            escena.add(circle);
            escena.add(cubo);
            escena.add(cubo1);
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