<template>

<div class="container">
    <h1>Tabla Login</h1>

    <table>

        <thead>
            <tr>
                <th>id</th>
                <th>username</th>
                <th>password</th>
            </tr>
        </thead>

        <tbody>

            <tr v-for="usuario in usuarios" :key="usuario.id">
                <td>{{ usuario.id }}</td>
                <td>{{ usuario.username }}</td>
                <td>{{ usuario.password }}</td>
            </tr>
        </tbody>

    </table>
</div>

</template>

<script>
import axios from 'axios';

export default {
    name: 'TablaLogin',
    data() {
        return {
            usuarios: []
        }
    },
    methods: {
        obtenerLogins() {
            axios.get('https://msa-project2-production.up.railway.app/api/login/listar')
                .then(response => {
                    this.usuarios = response.data;
                })
                .catch(error => {
                    console.error('Error al obtener los logins:', error);
                });
        }
    },
    mounted() {
        this.obtenerLogins();
    }
}

</script>