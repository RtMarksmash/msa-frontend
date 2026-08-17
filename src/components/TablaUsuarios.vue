<template>

<div class="container">
    <h1>Tabla Usuarios</h1>

    <table>

        <thead>
            <tr>
                <th>codigo</th>
                <th>nombre</th>
                <th>apellido</th>
                <th>tipo de sangre</th>
                <th>cargo</th>
                <th>email</th>
            </tr>
        </thead>

        <tbody>

            <tr v-for="usuario in usuarios" :key="usuario.id">
                <td>{{ usuario.id }}</td>
                <td>{{ usuario.nombre }}</td>
                <td>{{ usuario.apellido }}</td>
                <td>{{ usuario.tipoDeSangre }}</td>
                <td>{{ usuario.cargo }}</td>
                <td>{{ usuario.email }}</td>
            </tr>
        </tbody>

    </table>
</div>

</template>

<script>
import axios from 'axios';

export default {
    name: 'TablaUsuarios',
    data() {
        return {
            usuarios: []
        }
    },
    methods: {
        obtenerUsuarios() {
            axios.get('https://msa-project2-production.up.railway.app/api/usuarios/listar')
                .then(response => {
                    this.usuarios = response.data;
                })
                .catch(error => {
                    console.error('Error al obtener los usuarios:', error);
                });
        }
    },
    mounted() {
        this.obtenerUsuarios();
    }
}

</script>