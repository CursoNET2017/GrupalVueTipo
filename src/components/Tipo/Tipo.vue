<template>
  <div id="tipo">
    <div class="container">
        <h1>Tipos de Tareas Registradas</h1>
        <ul class="list-group">
            <a class="list-group-item" v-for="item in items" v-bind:key="item.Id" title="Seleccione una tipo para actualizar o borrar">
            {{item.Categoria}}
            </a>
        </ul>
        <button class="btn btn-info btn-responsive btninter">Nueva</button>
    </div>

  </div>
</template>

<script>


export default {
  name: 'entrada',
  data() {      
    return {
        items: [],
        visible : false,
        item:{id: '', categoria: '', descriptivo: '',repetitivo: '', silenciable: '',automatico: ''}
    };
  },
  methods: {   
    getTodos: function () {
        let _this = this;
        $.ajax({
            type: 'GET',
            url: 'http://localhost:51952/api/TipoTareas',
            success: function (response) {
                _this.items = JSON.parse(JSON.stringify(response));
                //_thhis.items = response;
            },
            error : function(){
                alert('Problemas al cargar el listado');
                debugger;
            }
        });
    }
  },
  created() {
      this.getTodos();
  }
}
</script>

<style>

.container {
    max-width: 80%;
}
</style>