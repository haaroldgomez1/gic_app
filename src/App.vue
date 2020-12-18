<template>
  <div id="app">
    <div style="width: 40%; padding: 5%;">
        <input id="input" type="number" autocomplete="off" spellcheck="false"  placeholder="Buscar un cliente por cédula" v-model="cli_cedula">
        <button id="boton" class="botonForm" v-on:click="BuscarCliente">Buscar</button>
        <h1>{{estado}}</h1>
    </div> 
    <Formulario v-bind:Clientes="listaUsuario"/>
  </div>
</template>

<script>
import Formulario from './components/Formulario.vue'
import axios from 'axios'
export default {
  name: 'App',
  components: {
    Formulario
  },
  data() {
    return {
      cli_cedula:0,
      listaUsuario: {
        "cli_cedula":0,
        "cli_nombre":'',
        "cli_telefono":0,
        "cli_correo":'',
        "cli_direccion":'',
        "cli_ciudad":''
      },
      estado:''
    }
  },
  methods: {
    BuscarCliente(){
      axios.get('http://127.0.0.1:8000/clientes/' + this.cli_cedula, {
    responseType: 'json' })
      .then(Response => {
      // Obtenemos los datos
      this.listaUsuario = Response.data;
      this.estado = 'Cliente encontrado'
      })
      .catch(e => {
        // Capturamos los errores
        console.log(e);
        this.listaUsuario = {
          "cli_cedula":0,
          "cli_nombre":'',
          "cli_telefono":0,
          "cli_correo":'',
          "cli_direccion":'',
          "cli_ciudad":''
        };
        this.estado = 'Cliente no encontrado'
      })
    }
  }
};
</script>

<style>
#app {
  height:100%;
  padding: 0%;
  margin: 0%;
  text-align: center;
  color: #2c3e50;
  background: rgb(131,58,180);
  background: linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(253,29,29,1) 50%, rgba(252,176,69,1) 100%);
  display: flex;
  position: relative;
  align-items: center;
}
#input {
    background-color: white;
    width: 90%;
    border: none;
    border-radius: 10px;
    font-size: 150%;
}
#boton{
    margin: 5px;
}
#boton {
    background-color:#7892c2;
	border-radius:28px;
	border:1px solid #4e6096;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Arial;
	font-size:17px;
	padding:16px 31px;
	text-decoration:none;
	text-shadow:0px 1px 0px #283966;
}
#boton:hover {
	background-color:#476e9e;
}
boton:active {
	position:relative;
	top:1px;
}#boton {
    background-color:#7892c2;
	border-radius:28px;
	border:1px solid #4e6096;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Arial;
	font-size:17px;
	padding:16px 31px;
	text-decoration:none;
	text-shadow:0px 1px 0px #283966;
}
#boton:hover {
	background-color:#476e9e;
}
boton:active {
	position:relative;
	top:1px;
}
</style>
