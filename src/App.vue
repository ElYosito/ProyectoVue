<script setup>
import { ref } from 'vue';

//Ocultar 
const ocultar = ref(true);

//Opcion del menu
const opcionSeleccionada = ref('');
const mostrarImagen = (opcion) => {
  opcionSeleccionada.value = opcion;
};

//modal
const texto = ref('');

//Ver mensaje
const mensaje = ref('');

const mostrarAlerta = () => {
  alert(`${mensaje.value}`);
};

//Tabla de multiplicar
const base = ref('');
const hasta = ref('');
const resultados = ref([]);
const mostrarResultado = ref(false);
const mostrarTablas = ref(false);

const calcularTablas = () => {
  resultados.value = [];
  mostrarResultado.value = false;

  if (!isNaN(base.value) && !isNaN(hasta.value)) {
    const baseNumero = parseInt(base.value);
    const hastaNumero = parseInt(hasta.value);

    for (let i = 1; i <= hastaNumero; i++) {
      resultados.value.push(`${baseNumero} x ${i} = ${baseNumero * i}`);
    }

    mostrarResultado.value = true;
  } else {
    alert('Por favor, ingrese números válidos en ambos campos.');
  }
};

const verTablas = () => {
  mostrarTablas.value = true;
};
</script>

<template>
  <header>
    <h1 class="display-1 d-flex justify-content-center">Practica 6</h1>
    <div class="d-flex justify-content-between">
      <p class="text-center text-white bg-primary rounded-3 lados">Pro web ll</p>
      <p class="text-center text-white bg-primary rounded-3 centro">Yosmar Coronado de
        los Reyes</p>
      <p class="text-center text-white bg-primary rounded-3 lados">Fw: VUE</p>
    </div>
  </header>

  <div class="bg-secondary rounded-3 ch">
    <div class="form-check form-switch chek">
      <input class="form-check-input" type="checkbox" id="show" v-model="ocultar">
      <label class="form-check-label text-white" for="show">
        Imagen Visible:
      </label>
    </div>
  </div>


  <br>

  <div class="row">
    <div class="col-2">
      <div class="accordion" id="accordionExample">
        <div class="accordion-item">
          <h2 class="accordion-header">
            <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne"
              aria-expanded="true" aria-controls="collapseOne">
              Galeria de fotos
            </button>
          </h2>
          <div id="collapseOne" class="accordion-collapse collapse show" data-bs-parent="#accordionExample">
            <div class="accordion-body">
              <div class="btn-group-vertical" role="group" aria-label="Vertical button group">
                <button type="button" class="btn btn-light" @click="mostrarImagen('Spiderman 1')">Spiderman 1</button>
                <button type="button" class="btn btn-light" @click="mostrarImagen('Spiderman 2')">Spiderman 2</button>
                <button type="button" class="btn btn-light" @click="mostrarImagen('Spiderman 3')">Spiderman 3</button>
                <button type="button" class="btn btn-light" @click="mostrarImagen('The amazing spiderman')">The amazing
                  spiderman</button>
              </div>
            </div>
          </div>
        </div>
        <div class="accordion-item">
          <h2 class="accordion-header">
            <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse"
              data-bs-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
              Ejercicios
            </button>
          </h2>
          <div id="collapseTwo" class="accordion-collapse collapse" data-bs-parent="#accordionExample">
            <div class="accordion-body">
              <div class="btn-group-vertical" role="group" aria-label="Vertical button group">
                <button type="button" class="btn btn-light" @click="mostrarImagen('modeloDiv')">Model</button>
                <button type="button" class="btn btn-light" @click="mostrarImagen('mensajeDiv')">Ver Mensaje</button>
                <button type="button" class="btn btn-light" @click="mostrarImagen('tablaDiv')">Tabla de
                  multiplicar</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="col-9">
      <div class="d-flex  justify-content-center">


        <!-- v-bind:style -->
        <h2 class="display-2" id="mensajeDesactivado" :style="{ display: !ocultar ? 'block' : 'none' }">Imagen desactivada
        </h2>

        <div id="ocultarDiv" :style="{ display: ocultar ? 'block' : 'none' }">
          <div id="VisualisarImagenes" v-show="opcionSeleccionada !== ''">
            <img v-if="opcionSeleccionada === 'Spiderman 1'" src="/images/spiderman1.jpg" alt="Spiderman 1">
            <img v-else-if="opcionSeleccionada === 'Spiderman 2'" src="/images/spiderman2.jpg" alt="Spiderman 2">
            <img v-else-if="opcionSeleccionada === 'Spiderman 3'" src="/images/spiderman3.jpg" alt="Spiderman 3">
            <img v-else-if="opcionSeleccionada === 'The amazing spiderman'" src="/images/TheAmazing.jpg"
              alt="The Amazing Spiderman">

            <div v-else-if="opcionSeleccionada === 'modeloDiv'" id="modeloDiv">
              <h2 class="display-6 text-center">Model:</h2>
              <input type="text" class="form-control" name="inputName" id="texto" v-model="texto" placeholder="Texto">

              <h3 class="display-6 text-center" id="copia">{{ texto }}</h3>

              <input type="text" class="form-control" name="inputName" id="copia" v-model="texto" readonly> <br>

              <p class="bg-primary text-center text-white rounded-3 copiap">{{ texto }}</p>
            </div>

            <div v-else-if="opcionSeleccionada === 'mensajeDiv'" id="mensajeDiv">
              <h4 class="display-6 text-center">Texto del mensaje:</h4>
              <input type="text" class="form-control" id="texto" v-model="mensaje" placeholder="Texto">

              <br>

              <div class="d-grid gap-2">
                <button type="button" name="" id="" class="btn btn-primary" @click="mostrarAlerta">Ver mensaje</button>
              </div>
            </div>

            <div v-else-if="opcionSeleccionada === 'tablaDiv'" id="tablaDiv">
              <h5 class="display-6 text-center ">Tablas de multiplicar</h5>
              <div class="container">
                <div class="mb-3 row">
                  <label for="base" class="col-4 col-form-label">Tabla de multiplicar:</label>
                  <div class="col-8">
                    <input type="text" class="form-control" v-model="base" @input="calcularTablas"
                      placeholder="Ingrese el número base">
                  </div>
                </div>

                <div class="mb-3 row">
                  <label for="hasta" class="col-4 col-form-label">Hasta que numero:</label>
                  <div class="col-8">
                    <input type="text" class="form-control" v-model="hasta" @input="calcularTablas"
                      placeholder="Ingrese el número hasta">
                  </div>
                </div>
              </div>

              <div class="d-grid gap-2">
                <button type="button" name="" id="" class="btn btn-primary" @click="verTablas">Ver tablas</button>
              </div>
              
              <br>
              
              <div id="mostrarTablas" v-if="mostrarTablas">
                <table class="table table-bordered">
                  <thead>
                    <tr>
                      <th class="text-center">Resultados</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-if="mostrarResultado" v-for="resultado in resultados" :key="resultado">
                      <td class="text-center">{{ resultado }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>

            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.lados {
  padding: 10px 90px 10px 90px;
}

.centro {
  padding: 10px 370px 10px 370px;
}

.ch {
  padding: 10px 0px 10px 0px;
}

.chek {
  margin: 0px 0px 0px 10px;
}

img {
  height: 300px;
  width: 200px;
}

#texto {
  width: 1000px;
}
</style>
