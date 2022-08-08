<template>
  <Titulo texto="Ruta con Parametros" />
  <h3 :class="{'red': mensajeError, 'blue': !mensajeError} ">{{ articulo.title }}</h3>
  <p>{{ articulo.body }}</p>

</template>

<script>

import Titulo from '../components/Titulo.vue'

export default {
    components: {
        Titulo,
    },
    data() {
      return {
          articulo: {},  
          mensajeError: false  
      }
    },
    methods: {
      async consumirArticulo() {
          try {
              const data = await fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
              const objeto = await data.json()
              if(this.$route.params.id > 100 || isNaN(this.$route.params.id) || this.$route.params.id <= 0 ) {
                this.mensajeError = true
                return this.articulo = { title: 'No encontramos este blog' }
              }
              this.mensajeError = false
              this.articulo = objeto;
          } catch (error) {
              console.log(error)
          }
      },

    },
    created() {
        this.consumirArticulo()
    }
}
</script>

<style>
 .red {
  color: brown;
  font-weight: bold;
  font-size: 30px;
 }
 .blue {
  color: dodgerblue;
 }
</style>