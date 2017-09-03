<template>
  <div class="container">
    <form id= "detalle" class="form-horizontal" v-on:submit.prevent="onSubmit">
        {{item}}
         <div class="form-group">
            <label class="col-sm-2 control-label">Categoria: </label>
            <div class="col-sm-10">
                <input name="categoria" type="text" placeholder="Introduce Categoria" v-model="item.categoria" class="form-control">
            </div>
        </div>
        <div class="form-group">
            <label class="col-sm-2 control-label">Descripción: </label>
            <div class="col-sm-10">
                <input name="descripcion" type="text" placeholder="Introduce una descripción" v-model="item.descripcion" class="form-control">
            </div>
        </div>
        <div class="form-group">
        <label for="checkbox" class="col-sm-10">
            <input type="checkbox" id="repetitivo" v-model="item.repetitivo">
            Repetitiva
        </label>
        <label for="checkbox" class="col-sm-10">
            <input type="checkbox" id="silenciable" v-model="item.silenciable">
            Silenciable
        </label>
        <label for="checkbox" class="col-sm-10">
            <input type="checkbox" id="automatico" v-model="item.automatico">
            Automatica
        </label>
        </div>
        <div id="botones" class="centrado">
            <button id="buttonCrear" v-on:click="crear" class="btn btn-success btn-responsive btninter">Añadir</button>
            <button id="buttonActualizar" v-on:click="actualizar" class="btn btn-success btn-responsive btninter">Actualizar</button>
            <button id="buttonBorrar" v-on:click="borrar" class="btn btn-success btn-responsive btninter">Borrar</button>
        </div>        
    </form>
    </div>
</template>


<script>

export default {
  name: 'detalle',
  props: ['item'],
  data() {
    return {
    };
  },
  methods: {
      crear: function(){
          this.$emit('crearH');
      },
      onSubmit: function(event){

      },
      actualizar: function(){
          this.$emit('actualizarH');
      },
      borrar: function(){
          this.$emit('borrarH');
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