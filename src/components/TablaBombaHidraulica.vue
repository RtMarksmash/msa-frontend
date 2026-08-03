<template>

<div class="container">
    <h1>Tabla Bomba Hidráulica</h1>

    <table>

        <thead>
            <tr>
                <th>id</th>
                <th>nombre</th>
                <th>marca</th>
                <th>altura dinamica</th>
                <th>caudal</th>
                <th>diametro de la succion</th>
                <th>diametro de la descarga</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="bomba in bombas" :key="bomba.id">
                <td>{{ bomba.id }}</td>
                <td>{{ bomba.nombre }}</td>
                <td>{{ bomba.marca }}</td>
                <td>{{ bomba.alturaDinamica }}</td>
                <td>{{ bomba.caudal }}</td>
                <td>{{ bomba.diametroSuccion }}</td>
                <td>{{ bomba.diametroDescarga }}</td>
            </tr>
        </tbody>
    </table>
</div>

</template>

<script>
import axios from 'axios';

export default {
    name: 'TablaBombaHidraulica',
    data() {
        return {
            bombas: []
        }
    },
    methods: {
        obtenerBombas() {
            axios.get('http://localhost:8080/api/bombas/listar')
                .then(response => {
                    this.bombas = response.data;
                })
                .catch(error => {
                    console.error('Error al obtener las bombas:', error);
                });
        }
    },
    mounted() {
        this.obtenerBombas();
    }
}
</script>