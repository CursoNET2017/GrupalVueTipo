<template>
  <div id="tipo">
    <div class="container">
        <div class="centrado">
            <h1>Tipos de Tareas</h1>
            <ul class="list-group">
                <a class="list-group-item" v-for="item in items" v-bind:key="item.Id" v-on:click="cargarClikMaestroH(item.Id)" title="Seleccione una tipo para actualizar o borrar">
                {{item.Categoria}}
                </a>
            </ul>
            <button v-on:click="visibleBorradoH" class="btn btn-success btn-responsive btninter">Nueva</button>
        </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'listado',
  props: ['items', 'item'],
  data() {      
    return {
    };
  },
  methods: {
      visibleBorradoH: function(){
          this.$emit('visibleBorradoH');
      },
      cargarClikMaestroH: function(refer){
          this.$emit('cargarClikMaestroH',refer);
      }
          
  }
}
</script>

<style>
.container {
    max-width: 80%;    
}
.centrado {
    text-align: center;
}
</style>