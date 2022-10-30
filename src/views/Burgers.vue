<template>

  <div id="App">

    <div class="container">

      <div class="row">

        

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


  },

  mounted() {

    this.GetApi();

  }

};
</script>

<style>
</style>
