<template>
  <section class="src-componentes-consulta">
    <div class="jumbotron">
      <h2>Pantalla de consulta</h2>
      <hr />
      <hr />
      <br />
      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>email</th>
            <th>telefono</th>
          </tr>
          <tr v-for="(dato, index) in datos" :key="index">
            <td>{{ dato.nombre }}</td>
            <td>{{ dato.email }}</td>
            <td>{{ dato.telefono }}</td>
          </tr>
        </table>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-consulta",
  props: [],
  mounted() {
    //this.getPostXHRcb()
    //this.getPostFetch()
    this.getDatosAxios();
  },
  data() {
    return {
      url: "https://6366a10cf5f549f052ca15a9.mockapi.io/datos/",
      datos: [],
    };
  },
  methods: {
    getUsuarios() {},
    getPostXHRcb() {
      const xhr = new XMLHttpRequest();
      xhr.open("get", this.url);
      xhr.addEventListener("load", () => {
        if (xhr.status == 200) {
          let respuesta = JSON.parse(xhr.response);
          console.log(respuesta);
          this.datos = respuesta;
        }
      });
      xhr.send();
    },
    async getPostFetch() {
      try {
        let response = await fetch(this.url);
        let respuesta = await response.json();
        console.log(respuesta);
        this.datos = respuesta;
      } catch (error) {
        console.error(error);
      }
    },
    async getDatosAxios() {
      try {
        let response = await this.axios(this.url);
        let respuesta = response.data;
        console.log(respuesta);
        this.datos = respuesta;
      } catch (error) {
        console.error(error);
      }
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: lightblue;
  color: black;
}

hr {
  background-color: white;
}

table{
  background-color: lightgreen;
  color:black;
}
</style>
