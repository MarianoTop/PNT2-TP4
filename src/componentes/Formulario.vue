<template>
  <section class="src-componentes-formulario">
    <div class="jumbotron">
      <h2>Pantalla de Formulario</h2>
      <hr />
      <hr />
      <br />

      <vue-form :state="formState" @submit.prevent="enviar()">
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input
            id="nombre"
            class="form-control"
            type="text"
            v-model.trim="formData.nombre"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            name="nombre"
            autocomplete="off"
          />
          <!-- cartel de validación -->
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <!---Pareceria no tener sentido el mensaje dado que evita ingresar mayor cantidad-->
            <div slot="maxlength" class="alert alert-danger mt-1">
              Este campo no debe poseer más de {{ nombreMaxLength }} caracteres.
            </div>
          </field-messages>
        </validate>
        <br />

        <!-- ------------------------------------------------------- -->
        <!-- Campo edad -->
        <validate tag="div">
          <label for="edad">Edad</label>
          <input
            id="edad"
            class="form-control"
            type="number"
            v-model.number="formData.edad"
            required
            name="edad"
            autocomplete="off"
            :min="edadMin"
            :max="edadMax"
          />
          <!-- cartel de validación -->
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="min" class="alert alert-danger mt-1">
              La edad mínima debe ser {{ edadMin }} años.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La edad máxima debe ser {{ edadMax }} años.
            </div>
          </field-messages>
        </validate>
        <br />

        <!-- ------------------------------------------------------- -->
        <!-- Campo email -->
        <validate tag="div">
          <label for="email">Email</label>
          <input
            id="email"
            class="form-control"
            type="email"
            v-model="formData.email"
            required
            name="email"
            autocomplete="off"
          />
          <!-- cartel de validación -->
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="email" class="alert alert-danger mt-1">
              Debe ingresar un email válido
            </div>
          </field-messages>
        </validate>
        <br />

        <!-- ------------------------------------------------------- -->
        <!-- Botón de envío -->
        <button class="btn btn-success my-3" :disabled="formState.$invalid">
          Enviar
        </button>
      </vue-form>
    </div>
    <div class="table-responsive">
      <table class="table table-dark">
        <tr>
          
          <th>Nombre</th>
          <th>Edad</th>
          <th>Mail</th>
        </tr>
        <tr v-for="(persona, index) in datosGuardados" :key="index">
          <td>{{ persona.nombre }}</td>
          <td>{{ persona.edad }}</td>
          <td>{{ persona.email }}</td>
        </tr>
      </table>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 5,
      nombreMaxLength: 15,
      edadMin: 18,
      edadMax: 120,
      datosGuardados: [],
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: null,
        edad: null,
        email: null,
      };
    },
    enviar() {
      console.log({ ...this.formData });
     

      const { nombre, edad,email }= { ...this.formData }
    
      this.datosGuardados.push({
       nombre,edad,email
        })
      this.formData = this.getInitialData();
      this.formState._reset();
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: red;
  color: white;
}

hr {
  background-color: black;
}
</style>
