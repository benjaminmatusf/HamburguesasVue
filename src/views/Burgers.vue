<template>

  <div id="App">

    <div class="container">

      <div class="row">

        <div class="col-md-3">

          <div class="card">
            <div class="card-body">

              <form>
                <div class="text-center mb-3">
                  <h4>CREAR NUEVA HAMBURGUESA</h4>
                </div>

                
                <div class="form-outline mb-4">
                  <input type="text" class="form-control" id="inputNombre" v-model="nombreX">
                  <label class="form-label" for="inputNombre">Nombre</label>
                </div>

                
                <div class="form-outline mb-4">
                  <input type="text" class="form-control" id="inputIngredientes" v-model="ingredientesX">
                  <label class="form-label" for="inputIngredientes">Ingredientes</label>
                </div>

               
                <div class="form-outline mb-4">
                  <input type="number" class="form-control" id="inputCalorias" v-model="caloriasX">
                  <label class="form-label" for="inputCalorias">Calorias</label>
                </div>


                
                <button type="submit" class="btn btn-success btn-block mb-4" v-on:click="PostApi()">Crear</button>
              </form>

            </div>
          </div>



        </div>

        <div class="col-md-9">
          <div class="table-responsive">
            <table class="table table-striped">

              <thead>
                <tr>
                  <th>Id</th>
                  <th>Nombre</th>
                  <th>Ingredientes</th>
                  <th>Calorias</th>

                </tr>
              </thead>

              <tbody>
                <tr v-for="item of items" v-bind:key="item.id">
                  <td>{{ item.id }}</td>
                  <td><input type="text" v-model="item.nombre" /> </td>
                  <td><input type="text" v-model="item.ingredientes" style="width:500px" /></td>
                  <td><input type="text" v-model="item.calorias" /></td>
                 
                </tr>
              </tbody>

            </table>
          </div>
        </div>

      </div>

    </div>

  </div>

</template>


<script>

import axios from "axios";
const baseUrl = "https://prueba-hamburguesas.herokuapp.com/burger/";

export default {

  name: "Burgers",

  data() {

    return {

      items: [],
      idX: '',
      nombreX: '',
      ingredientesX: [" "],
      caloriasX: '',
    }

  },

  methods: {

    async GetApi() {

      await axios

        .get(baseUrl)

        .then((resp) => {

          this.items = resp.data;

        })

        .catch((err) => {

          console.log(err);

        });

    },

async PostApi() {

  await axios

    .post(baseUrl, {
      nombre: this.nombreX,
      ingredientes: [this.ingredientesX],
      calorias: this.caloriasX
    })

    .then((resp) => {

      console.log(resp);

      this.nombreX = '';
      this.ingredientesX = '';
      this.caloriasX = '';

      this.GetApi();

    })

    .catch((err) => {

      console.log(err);

    });

},


  },

  mounted() {

    this.GetApi();

  }

};
</script>

<style>
</style>
