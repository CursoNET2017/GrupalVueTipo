<template>
<div id="tipo">
    <listado v-bind:items="items" v-on:visibleBorradoH="visibleBorrado" v-on:cargarClikMaestroH="cargarClikMaestro"></listado>
    <detalle v-show="visible" v-bind:item="item" v-on:crearH="crear" v-on:actualizarH="actualizar" v-on:borrarH="borrar"></detalle>
</div>
</template>

<script>
import listado from './TipoListado.vue'
import detalle from './TipoDetalle.vue'


export default {
  name: 'tipo',
  data() {      
    return {
        items: [],
        visible : false,
        item:{id: '', categoria: '', descripcion: '',repetitivo: '', silenciable: '',automatico: ''}
    };
  },
  components: {
      listado, detalle
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
		        _this.getTodos();
		    }
        });
    },
    actualizar: function(){
        var id1 = this.item.id;
        let _this = this;
	  	$.ajax({
		    url : 'http://localhost:51952/api/TipoTareas/'+id1,
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
		        _this.getTodos();
		    }
	  	});
    },
    borrar: function(){
        let id1 = this.item.id;
        let categoria1 = this.item.categoria;
        let _this = this;
        $.ajax({
            type: 'DELETE',
            url: 'http://localhost:51952/api/TipoTareas/'+id1,
            success: function () {
                _this.visibleBorrado();
            },
            error : function(){
                alert('Problemas al borrar el item');
                debugger;
            },
            complete : function() {
                _this.getTodos();
                alert('Eliminado con exito '+categoria1);
            }
        })
    }    
  },
  created() {
      this.getTodos();
  }
}
</script>

<style>  

</style>