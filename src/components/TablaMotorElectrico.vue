<template>

<div class="container">
    <h1>Tabla Motor</h1>

    <table>

        <thead>
            <tr>
                <th>id</th>
                <th>nombre</th>
                <th>marca</th>
                <th>amperaje</th>
                <th>voltaje</th>
                <th>motor potencia</th>
                <th>rodamientos</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="motor in motores" :key="motor.id">
                <td>{{ motor.id }}</td>
                <td>{{ motor.nombre }}</td>
                <td>{{ motor.marca }}</td>
                <td>{{ motor.amperaje }}</td>
                <td>{{ motor.voltaje }}</td>
                <td>{{ motor.motorPotencia }}</td>
                <td>{{ motor.rodamientos }}</td>
            </tr>
        </tbody>
    </table>
</div>

</template>

<script>
import axios from 'axios';

export default {
    name: 'TablaMotorElectrico',
    data() {
        return {
            motores: []
        }
    },
    methods: {
        obtenerMotores() {
            axios.get('http://localhost:8080/api/motores/listar')
                .then(response => {
                    this.motores = response.data;
                })
                .catch(error => {
                    console.error('Error al obtener los motores:', error);
                });
        }
    },
    mounted() {
        this.obtenerMotores();
    }
}

</script>