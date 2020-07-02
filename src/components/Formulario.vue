<template>

  <section class="src-components-formulario">
    <div class="jumbotron mt-3">
    <h1>src-components-formulario Component</h1>
     <vue-form :state="formState" @submit.prevent="enviar()">


      <validate tag="div">
        <label for="descripcion">Descripcion</label>
        <input 
          type="text"
          id="descripcion"
          class="form-control"
          autocomplete="off"
          name="descripcion"
          v-model.trim="formData.descripcion"
          required
          no-espacios
          :minlength="charMinNombre"
          :maxlength="charMaxNombre"
        >
        <field-messages name="descripcion" show="$dirty">
          <div slot="required" class="alert alert-danger my-1">Campo descripcion requerido</div>
          <div slot="no-espacios" class="alert alert-danger my-1">No se permiten espacios intermedios en este campo</div>
          <div slot="minlength" class="alert alert-danger my-1">Se deben ingresar como minimo {{charMinNombre}}</div>
          <div v-if="formData.nombre.length == charMaxNombre" class="alert alert-danger my-1">Se deben ingresar como minimo {{charMaxNombre}}</div>
        </field-messages>


      </validate>
      <br>

      <validate tag="div">
        <label for="nombre">Nombre</label>
        <input 
          type="text"
          id="nombre"
          class="form-control"
          autocomplete="off"
          name="nombre"
          v-model.trim="formData.nombre"
          required
        >
        <field-messages name="nombre" show="$dirty">
          <!-- <div class="alert alert-success my-1">Campo correcto</div> -->
          <div slot="required" class="alert alert-danger my-1">Campo nombre requerido</div>
        </field-messages>

      </validate>        
      <br>

      <validate tag="div">
        <label for="email">Email</label>
        <input 
          type="email"
          id="email"
          class="form-control"
          autocomplete="off"
          name="email"
          v-model="formData.email"
          required
        >
        <field-messages name="email" show="$dirty">
          <div slot="required" class="alert alert-danger my-1">Campo email requerido</div>
          <div slot="email" class="alert alert-danger my-1">El email es invalido</div>
        </field-messages>
      </validate>
      <br>

      <button class="btn btn-success my-4" :disabled="formState.$invalid || enviando" type="submit">Enviar</button>
      <br>
      </vue-form>
      <Listado />
    </div>
  </section>

</template>

<script lang="js">
  import axios from 'axios'
  import Listado from './Listado.vue';
  const url = 'https://5ee29b1e8b27f30016094cf8.mockapi.io/tareas'
  export default  {
    name: 'Formulario',
    omponents : {
      Listado
    },
    props: [],
    mounted () {

    },
    data () {
      return {
        tareas: [],
        formState : {},
        formData : this.getInitialData(),
        enviando: false,
        charMinNombre: 3,
        charMaxNombre: 15
      }
    },
    methods: {
      getInitialData() {
      return {
        descripcion: '',
        nombre: '',
        email: ''
      }
    },
        enviar() {
      this.enviando = true
      console.log(this.formData)
      axios.post(url, this.formData,{
        'content-type' : 'application.json'
      })
      .then( res =>{
        console.log(res.data)
        this.formData = this.getInitialData()
        this.formState._reset()
        this.enviando = false
      })
      .catch(error=>{
        console.log(error)
        
      })
      
      }

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-formulario {}
    .jumbotron {
    background-color: rgb(173, 35, 62);
    color: white;
  }

  hr {
      background-color: white;
    }

  pre {
      color: white;
    }
  
</style>
