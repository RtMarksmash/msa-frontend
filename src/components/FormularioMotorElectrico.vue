<template>
    <div class="container">
        <h1>Formulario Motores</h1>

        <form action="" id="student-form" @submit.prevent="guardar">

               <div class="form-group">
                <label for="Id">Id:</label>
                <input type="text" id="Id" v-model="Id" name="Id" required>
            </div>

            <div class="form-group">
                <label for="nombre">nombre:</label>
                <input type="text" id="nombre" v-model="nombre" name="nombre" required>
            </div>

            <div class="form-group">
                <label for="marca">marca:</label>
                <input type="text" id="marca" v-model="marca" name="marca" required>
            </div>

            <div class="form-group">
                <label for="amperaje">amperaje:</label>
                <input type="text" id="amperaje" v-model="amperaje" name="amperaje" required>
            </div>

             <div class="form-group">
                <label for="voltaje">voltaje:</label>
                <input type="text" id="voltaje" v-model="voltaje" name="voltaje" required>
            </div>
            <div class="form-group">
                <label for="motorPotencia">potencia del motor:</label>
                <input type="text" id="motorPotencia" v-model="motorPotencia" name="motorPotencia" required>
            </div>

            <div class="form-group">
                <label for="rodamientos">rodamientos:</label>
                <input type="text" id="rodamientos" v-model="rodamientos" name="rodamientos" required>
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
    name: 'FormularioMotorElectrico',
    data() {
        return {
            Id: '',
            nombre: '',
            marca: '',
            amperaje: '',
            voltaje: '',
            motorPotencia: '',
            rodamientos: '',
        }
    },
    methods: {
        guardar() {
            const motor = {
                nombre: this.nombre,
                marca: this.marca,
                amperaje: this.amperaje,
                voltaje: this.voltaje,
                motorPotencia: this.motorPotencia,
                rodamientos: this.rodamientos,
                
            };

            axios.post('http://localhost:8080/api/motores', motor)
                .then(response => {
                    console.log('motor guardado:', response.data);
                    alert('Motor guardado exitosamente');
                    this.Id = '';
                    this.nombre = ''; 
                    this.marca = '';
                    this.amperaje = '';
                    this.voltaje = '';
                    this.motorPotencia = '';
                    this.rodamientos = '';
                    this.$emit('actualizar-tabla');  
                   
                })
                .catch(error => {
                    console.error('Error al guardar el motor:', error);
                    alert('Error al guardar el motor');
                    
                });
        },
        consultar() {
            axios.get('http://localhost:8080/api/motores/' + this.Id)
                .then(response => {
                    console.log('motores consultados:', response.data);
                    this.Id = response.data.id || this.Id;
                    this.nombre = response.data.nombre;
                    this.marca = response.data.marca;
                    this.amperaje = response.data.amperaje;
                    this.voltaje = response.data.voltaje;
                    this.motorPotencia = response.data.motorPotencia;
                    this.rodamientos = response.data.rodamientos;
                })
                .catch(error => {
                    console.error('Error al consultar los motores:', error);
                    alert('Error al consultar los motores');
                    
                });
        },
        actualizar() {
            const motor = {
                id: this.Id,
                nombre: this.nombre,
                marca: this.marca,
                amperaje: this.amperaje,
                voltaje: this.voltaje,
                motorPotencia: this.motorPotencia,
                rodamientos: this.rodamientos,
            };

            axios.put('http://localhost:8080/api/motores/actualizar/' + this.Id, motor)
                .then(response => {
                    console.log('Motor actualizado:', response.data);
                    alert('Motor actualizado exitosamente');
                    this.$emit('actualizar-tabla');
                })
                .catch(error => {
                    console.error('Error al actualizar el motor:', error);
                    alert('Error al actualizar el motor');
                });
        },
        eliminar() {
            axios.delete('http://localhost:8080/api/motores/' + this.Id)
                .then(response => {
                    console.log('Motor eliminado:', response.data);
                    alert('Motor eliminado exitosamente');
                    this.Id = '';
                    this.nombre = ''; 
                    this.marca = '';
                    this.amperaje = '';
                    this.voltaje = '';
                    this.motorPotencia = '';
                    this.rodamientos = '';
                    this.$emit('actualizar-tabla');
                    
                })
                .catch(error => {
                    console.error('Error al eliminar el motor:', error);
                    alert('Error al eliminar el motor');
                    
                });
        }
    }
}

</script>