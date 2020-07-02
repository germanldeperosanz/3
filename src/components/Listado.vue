<template>

  <section class="src-components-listado">
    <div class="jumbotron mt-3">
    <table class="table">
              <tr class="bg-success text-white">
                  <th>ID</th>
                  <th>Descripcion</th>
                  <th>Nombre</th>
                  <th>Email</th>
              </tr>
              <tr class="bg-info text-white" v-for="(dato,index) in formData" :key="index">
                  <td>{{dato.id}}</td>
                  <td>{{ dato.descripcion }}</td>
                  <td>{{ dato.nombre }}</td>
                  <td>{{ dato.email }}</td>
              </tr>
          </table>
      <br>
    </div>
  </section>

</template>

<script lang="js">
  import axios from 'axios'
  const urlTp4 = 'https://5ee29b1e8b27f30016094cf8.mockapi.io/tareas/'

  export default  {
    name: 'Listado',
    props: [],
    mounted () {
      axios.get(urlTp4)
      .then(res => {
        console.log(res.data)
        this.formData= res.data})
      .catch(error=>{
        console.log('error get', error)  
      })
    },
    data () {
      return {
        formData : [] 
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-listado {

  }
  .jumbotron {
    background-color: blue;
    color: white;
  }

  hr {
    background-color: #ddd;
  }
</style>
