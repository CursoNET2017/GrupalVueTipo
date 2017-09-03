<template>
  <div id="tipo">
    <div class="container">
        <div class="centrado">
            <h1>Tipos de Tareas</h1>
            <ul class="list-group">
                <a class="list-group-item" v-for="item in items" v-bind:key="item.Id" v-on:click="cargarClikMaestro(item.Id)" title="Seleccione una tipo para actualizar o borrar">
                {{item.Categoria}}
                </a>
            </ul>
            <button v-on:click="visibleBorrado" class="btn btn-info btn-responsive btninter">Nueva</button>
        </div>
    </div>
<!-- DETALLE -->
    <div class="container">
    <form id= "detalle" class="form-horizontal" v-show="visible" v-on:submit.prevent="onSubmit">
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
            <button id="buttonCrear" v-on:click="crear" class="btn btn-info btn-responsive btninter">Añadir</button>
            <button id="buttonActualizar" v-on:click="actualizar" class="btn btn-info btn-responsive btninter">Actualizar</button>
            <!--
            <button id="buttonBorrar" v-on:click="borrar" class="btn btn-info btn-responsive btninter">Borrar</button>
            -->
        </div>        
    </form>
    </div>
  </div>
</template>

<script>

export default {
  name: 'tipo',
  data() {      
    return {
        items: [],
        visible : false,
        item:{id: '', categoria: '', descripcion: '',repetitivo: '', silenciable: '',automatico: ''}
    };
  },
  methods: {   
    getTodos: function () {
        let _this = this;
        $.ajax({
            type: 'GET',
            url: 'http://localhost:51952/api/TipoTareas',
            success: function (response) {
                //_this.items = JSON.parse(JSON.stringify(response));
                _this.items = response;
            },
            error : function(){
                alert('Problemas al cargar el listado');
                debugger;
            }
        });
    },
    visibleBorrado: function() {
        //this.visible = !this.visible;
        this.visible = true;
        this.item.id = '';
        this.item.categoria = '';
        this.item.descripcion = '';
        this.item.repetitivo = false;
        this.item.silenciable = false;
        this.item.automatico = false;
    },
    cargarClikMaestro: function(refer){
        let _this = this;
        $.ajax({
            url: 'http://localhost:51952/api/TipoTareas/'+refer,
            type : 'GET',     
            success : function(response) {
            //alert('YUPII');
            _this.rellenarDatosClick(response);
            },
            error : function(){
            debugger;
            }
        });
    },
    rellenarDatosClick: function(response) {
        this.visible = true;        
        this.item.id = response.Id;
        this.item.categoria = response.Categoria;
        this.item.descripcion = response.Descripcion;
        this.item.repetitivo = response.Repetitivo;
        this.item.silenciable = response.Silenciable;
        this.item.automatico = response.Automatico;
    },
    onSubmit: function(event){
        alert('onSubmit');
        this.getTodos();
    },
    crear: function() {
        let _this = this;
        let categoria1 = this.item.categoria;
        let descripcion1 = this.item.descripcion;
        let repetitivo1 = this.item.repetitivo;
        let silenciable1 = this.item.silenciable;
        let automatico1 = this.item.automatico;
        $.ajax({
            type: 'POST',
            url: 'http://localhost:51952/api/TipoTareas/',
            data: {Categoria: categoria1, Descripcion: descripcion1, Repetitivo: repetitivo1, Silenciable: silenciable1, Automatico: automatico1},
            success: function (response) {
                //_this.getTodos();
                _this.visibleBorrado();
            },
            error : function(){
                alert('Problemas al insertar el item');
                debugger;
            },        
		    complete : function(xhr, status) {
		        //alert('Creado '+titulo1+' con exito');
		        //_this.getTodos();
		    }
        });
    },
    actualizar: function(){
        var id1 = this.item.id;
    	var nombre1 = this.item.nombre;
	  	var apellidos1 = this.item.apellidos;
	  	alert(nombre1+' '+apellidos1);
        let _this = this;
	  	$.ajax({
		    url : 'http://localhost:50422/api/Entradas/'+id1,
		    type : 'PUT',     
		    dataType : 'json',
            data: _this.item,
		    success : function(response) {            
		        _this.visibleBorrado();
		    },
		    error : function(){
		    	alert('CACA');
		     	debugger;
		    },        
		    complete : function(xhr, status) {
		        //alert('Actualización con exito');
		        //_this.getTodos();
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
.centrado {
    text-align: center;
}
</style>