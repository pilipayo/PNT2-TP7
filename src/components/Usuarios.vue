<template>
  <section class="src-components-usuarios">
    <div class="jumbotron">
    <h3>Usuarios agregados</h3>
    <hr>
   
   <button class="btn btn-light mr-2 mb-3" @click="getIngresos()">Ver ingresos</button>
  

    <div v-if="!ingresos.length">
      <div class="alert alert-danger">
        No hay usuarios para mostrar
      </div>
    </div>


    <table v-else class="table table-striped table-dark">
      <thead>
        <tr>
          <th scope="col">Nombre</th>
          <th scope="col">Edad</th>
          <th scope="col">Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(ingreso, index) in ingresos" :key="index">
          <td>{{ ingreso.nombre }}</td>
          <td>{{ ingreso.edad }}</td>
          <td>{{ ingreso.email }}</td>
        </tr>
      </tbody>
    </table>
      </div>
     
  </section>

</template>

<script>
  export default  {
    name: 'src-components-vista',
    props: [],
    beforeMount() {
    this.getIngresos();
  },
    data () {
      return {
        url: "https://62966e8f810c00c1cb75b66a.mockapi.io/ingresos",
        ingresos: []
      }
    },
    methods: {
      async getIngresos() {
        try {
          let { data: ingresos } = await this.axios(this.url)
          console.log('AXIOS GET ingresos', ingresos)
          this.ingresos = ingresos
        }
        catch(error) {
          console.error('Hubo un error en getIngresos()', error.message)
        }
      },
    },
    computed: {
    }
}
</script>

<style scoped lang="css">
  .jumbotron {
  color: black;
  background-color: rgb(236, 226, 195);
  }
  .table-striped tbody tr:nth-of-type(odd) {
  background-color: rgb(197, 189, 151);
  }
  .table-striped tbody tr:nth-of-type(even) {
    background-color: rgb(120, 112, 76);
  }
</style>
