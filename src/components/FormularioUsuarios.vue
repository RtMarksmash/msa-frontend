<template>

    <div class="container">
        <h1>Formulario Usuarios</h1>

        <form action="" id="student-form" @submit.prevent="guardar">

            <div class="form-group">
                <label for="Id">Id:</label>
                <input type="text" id="Id" v-model="Id" name="Id">
            </div>

            <div class="form-group">
                <label for="nombre">nombre:</label>
                <input type="text" id="nombre" v-model="nombre" name="nombre" required>
            </div>

            <div class="form-group">
                <label for="apellido">apellido:</label>
                <input type="text" id="apellido" v-model="apellido" name="apellido" required>
            </div>

            <div class="form-group">
                <label for="TipoDeSangre">Tipo de Sangre:</label>
                <input type="text" id="TipoDeSangre" v-model="TipoDeSangre" name="TipoDeSangre" required>
            </div>

             <div class="form-group">
                <label for="Cargo">Cargo:</label>
                <input type="text" id="Cargo" v-model="Cargo" name="Cargo" required>
            </div>
            <div class="form-group">
                <label for="Email">Email:</label>
                <input type="text" id="Email" v-model="Email" name="Email" required>
            </div>

            <button type="submit">Guardar</button><br>
            <button type="button" @click="eliminar">Eliminar</button><br>
            <button type="button" @click="actualizar">Actualizar</button><br>
            <button type="button" @click="consultar">Consultar</button><br>

        </form>
    </div>

</template>

<script>
import axios from 'axios';

export default {
    name: 'FormularioUsuarios',
    data() {
        return {
            Id: '',
            nombre: '',
            apellido: '',
            TipoDeSangre: '',
            Cargo: '',
            Email: '',
        }
    },
    methods: {
        guardar() {
            const usuario = {
                id: this.Id,
                nombre: this.nombre,
                apellido: this.apellido,
                tipoDeSangre: this.TipoDeSangre,
                cargo: this.Cargo,
                email: this.Email
            };

            axios.post('http://localhost:8080/api/usuarios', usuario)
                .then(response => {
                    console.log('usuario guardado:', response.data);
                    alert('Usuario guardado exitosamente');
                    this.Id = '';
                    this.nombre = ''; 
                    this.apellido = '';
                    this.TipoDeSangre = '';
                    this.Cargo = '';
                    this.Email = '';
                    this.$emit('actualizar-tabla');  
                   
                })
                .catch(error => {
                    console.error('Error al guardar el usuario:', error);
                    alert('Error al guardar el usuario');
                    
                });
        },
        consultar() {
            axios.get('http://localhost:8080/api/usuarios/' + this.Id)
                .then(response => {
                    console.log('Usuarios consultados:', response.data);
                    this.Id = response.data.id || this.Id;
                    this.nombre = response.data.nombre;
                    this.apellido = response.data.apellido;
                    this.TipoDeSangre = response.data.tipoDeSangre;
                    this.Cargo = response.data.cargo;
                    this.Email = response.data.email;
                })
                .catch(error => {
                    console.error('Error al consultar los usuarios:', error);
                    alert('Error al consultar los usuarios');
                    
                });
        },
        actualizar() {
            const usuario = {
                id: this.Id,
                nombre: this.nombre,
                apellido: this.apellido,
                tipoDeSangre: this.TipoDeSangre,
                cargo: this.Cargo,
                email: this.Email,
            };

            axios.put('http://localhost:8080/api/usuarios/actualizar/' + this.Id, usuario)
                .then(response => {
                    console.log('Usuario actualizado:', response.data);
                    alert('Usuario actualizado exitosamente');
                    this.$emit('actualizar-tabla');
                })
                .catch(error => {
                    console.error('Error al actualizar el usuario:', error);
                    alert('Error al actualizar el usuario');
                    
                });
        },
        eliminar() {
            axios.delete('http://localhost:8080/api/usuarios/' + this.Id)
                .then(response => {
                    console.log('Usuario eliminado:', response.data);
                    alert('Usuario eliminado exitosamente');
                    this.Id = '';
                    this.nombre = ''; 
                    this.apellido = '';
                    this.TipoDeSangre = '';
                    this.Cargo = '';
                    this.Email = '';
                    this.$emit('actualizar-tabla');
                    
                })
                .catch(error => {
                    console.error('Error al eliminar el usuario:', error);
                    alert('Error al eliminar el usuario');
                    
                });
        }
    }
}

</script>