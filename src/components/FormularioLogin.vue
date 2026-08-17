<template>
    <div class="container">
        <h1>Formulario Login</h1>

        <form action="" id="student-form" @submit.prevent="guardar">

            <div class="form-group">
                <label for="Id">Id:</label>
                <input type="text" id="Id" v-model="Id" name="Id">
            </div>

            <div class="form-group">
                <label for="username">username:</label>
                <input type="text" id="username" v-model="username" name="username" required>
            </div>

            <div class="form-group">
                <label for="password">password:</label>
                <input type="text" id="password" v-model="password" name="password" required>
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
    name: 'FormularioLogin',
    data() {
        return {
            Id: '',
            username: '',
            password: '',
        }
    },
    methods: {
        guardar() {
            const login = {
                username: this.username,
                password: this.password
            };

            axios.post('http://msa-project2-production.up.railway.app/api/login', login)
                .then(response => {
                    console.log('login guardado:', response.data);
                    alert('Login guardado exitosamente');
                    this.Id = '';
                    this.username = ''; 
                    this.password = '';
                    this.$emit('actualizar-tabla');  
                   
                })
                .catch(error => {
                    console.error('Error al guardar el login:', error);
                    alert('Error al guardar el login');
                    
                });
        },
        consultar() {
            axios.get('http://msa-project2-production.up.railway.app/api/login/' + this.Id)
                .then(response => {
                    console.log('Login consultados:', response.data);
                    this.Id = response.data.id || this.Id;
                    this.username = response.data.username;
                    this.password = response.data.password;
                })
                .catch(error => {
                    console.error('Error al consultar los usuarios:', error);
                    alert('Error al consultar los usuarios');
                    
                });
        },
        actualizar() {
            const login = {
                username: this.username,
                password: this.password
            };

            axios.put('http://localhost:8080/api/login/actualizar/' + this.Id, login)
                .then(response => {
                    console.log('Login actualizado:', response.data);
                    alert('Login actualizado exitosamente');
                    this.$emit('actualizar-tabla');
                })
                .catch(error => {
                    console.error('Error al actualizar el login:', error);
                    alert('Error al actualizar el login');
                    
                });
        },
        eliminar() {
            axios.delete('http://localhost:8080/api/login/' + this.Id)
                .then(response => {
                    console.log('Login eliminado:', response.data);
                    alert('Login eliminado exitosamente');
                    this.Id = '';
                    this.username = ''; 
                    this.password = '';
                    this.$emit('actualizar-tabla');
                    
                })
                .catch(error => {
                    console.error('Error al eliminar el login:', error);
                    alert('Error al eliminar el login');
                    
                });
        }
    }
}

</script>