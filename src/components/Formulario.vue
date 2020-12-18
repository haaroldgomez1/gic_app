<template>
        <div id="Formulario">
            <h2 id="titulo"> Cliente </h2>
            <form  id="contenido">
                <div class="form-group">
                    <label for="nombreCliente">Nombre Cliente</label>
                    <input type="text" class="inputForm" id="nombreCliente" placeholder="Escriba el nombre del cliente" v-model="Clientes.cli_nombre">
                </div>
                <div class="form-group">
                    <label for="cedula">Cédula Cliente</label>
                    <input type="number" class="inputForm" id="cedula" placeholder="Escriba la cédula del cliente" v-model="Clientes.cli_cedula">
                </div>
                <div class="form-group">
                    <label for="telefono">Teléfono Cliente</label>
                    <input type="number" class="inputForm" id="telefono" placeholder="Escriba el teléfono del cliente" v-model="Clientes.cli_telefono">
                </div>  
                <div class="form-group">
                    <label for="correo">Correo Cliente</label>
                    <input type="text" class="inputForm" id="correo" placeholder="Escriba el correo del cliente" v-model="Clientes.cli_correo">
                </div>   
                <div class="form-group">
                    <label for="direccion">Dirección Cliente</label>
                    <input type="text" class="inputForm" id="direccion" placeholder="Escriba la dirección del cliente" v-model="Clientes.cli_direccion">
                </div> 
                <div class="form-group">
                    <label for="ciudad">Ciudad Cliente</label>
                    <input type="text" class="inputForm" id="Ciudad" placeholder="Escriba la ciudad del cliente" v-model="Clientes.cli_ciudad">
                </div>          
                <div class="form-group">
                    <br/>
                    <br/>
                    <button class="botonForm" v-on:click.prevent="submitForm">Crear</button>
                    <button class="botonForm" v-on:click.prevent="actualizarCliente">Actualizar</button>
                </div>
                <div>
                    <h1>{{estado}}</h1>
                </div>
            </form>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Formulario',
    components: {
    },
    data () {
        return{
            estado:''
        }
    },
    props: {
        Clientes:Object,
        compras:Object
    },
    methods:{
        submitForm(){
            console.log(this.form)
            axios.post('http://127.0.0.1:8000/clientes', this.Clientes)
                 .then((res) => {
                     console.log(res.data);
                     this.estado = 'Se creó el usuario'
                 })
                 .catch(() => {
                     this.estado = 'Hubo error. No se creó el usuario'
                 }).finally(() => {
                     
                 });
        },
        actualizarCliente(){
            console.log(this.form)
            axios.put('http://127.0.0.1:8000/clientes', this.Clientes)
                 .then((res) => {
                     console.log(res.data);
                     this.estado = 'Se actualizó el usuario'
                 })
                 .catch(() => {
                     this.estado = 'Hubo error. No se actualizó el usuario'
                 }).finally(() => {
                     
                 });
        }
    }
}
</script>

<style>
#Formulario {
    width: 50%;
    height: 80%;
    position: relative;
    right: 5%;
    top: 5%;
    bottom: 5%;
    background: rgb(255,255,255);
    background: radial-gradient(circle, rgba(255,255,255,1) 2%, rgba(61,154,255,1) 100%, rgba(26,136,255,1) 100%);
    border-radius: 10px;
}
#titulo {
    position: relative;
    top: 10%;
}
#contenido {
    position: relative;
    top: 20%;
}
.inputForm {
    width: 40%;
    margin: 5px;
    position: relative;
    top: 15%;
    right: -10%;
    border-radius: 10px;
    height: 5%;
    text-align: center;
}
.botonForm {
    border-radius: 10px;
    margin-left: 30px;
}


</style>