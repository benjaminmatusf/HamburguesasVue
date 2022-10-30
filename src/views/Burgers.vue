<template>

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
                  <th>Actualizar</th>
                  <th>Eliminar</th>
                </tr>
              </thead>

              <tbody>
                <tr v-for="todo of todos" v-bind:key="todo.id">
                  <td>{{ todo.id }}</td>
                  <td><input type="text" v-model="todo.nombre" /> </td>
                  <td><input type="text" v-model="todo.ingredientes" style="width:500px" /></td>
                  <td><input type="text" v-model="todo.calorias" /></td>
                  <td><button class="btn btn-success text-white" v-on:click="PutApi(todo.id, todo.nombre, todo.ingredientes, todo.calorias)">Update</button>
                  </td>
                  <td><button class="btn btn-danger text-white" v-on:click="DeleteApi(todo.id)">Delete</button></td>
                </tr>
              </tbody>

            </table>
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

      todos: [],
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

          this.todos = resp.data;

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

    async DeleteApi(id) {

      await axios

        .delete(baseUrl + id)

        .then((resp) => {

          console.log(resp);

          this.GetApi();

        })

        .catch((err) => {

          console.log(err);

        });

    },

    async PutApi(id, nombre, ingredientes, calorias) {


      await axios

        .put(baseUrl + id, {
          nombre: nombre,
          ingredientes: ingredientes,
          calorias: calorias,
        })

        .then((resp) => {

          console.log(resp);
          this.GetApi();

        })

        .catch((err) => {

          console.log(err);

        });

    }

  },

  mounted() {

    this.GetApi();

  }

};

</script>



<style>

</style>