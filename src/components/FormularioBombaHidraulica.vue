<template>
    <div class="container">
        <h1>Formulario Bombas</h1>

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
                <label for="marca">marca:</label>
                <input type="text" id="marca" v-model="marca" name="marca" required>
            </div>

            <div class="form-group">
                <label for="alturaDinamica">altura dinámica:</label>
                <input type="text" id="alturaDinamica" v-model="alturaDinamica" name="alturaDinamica" required>
            </div>

             <div class="form-group">
                <label for="caudal">caudal:</label>
                <input type="text" id="caudal" v-model="caudal" name="caudal" required>
            </div>
            <div class="form-group">
                <label for="diametroDeSuccion">diámetro de succión:</label>
                <input type="text" id="diametroDeSuccion" v-model="diametroDeSuccion" name="diametroDeSuccion" required>
            </div>

            <div class="form-group">
                <label for="diametroDeDescarga">diámetro de descarga:</label>
                <input type="text" id="diametroDeDescarga" v-model="diametroDeDescarga" name="diametroDeDescarga" required>
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
    name: 'FormularioBombaHidraulica',
    data() {
        return {
            Id: '',
            nombre: '',
            marca: '',
            alturaDinamica: '',
            caudal: '',
            diametroDeSuccion: '',
            diametroDeDescarga: '',
        }
    },
    methods: {
        guardar() {
            const bomba = {
                id: this.Id,
                nombre: this.nombre,
                marca: this.marca,
                alturaDinamica: this.alturaDinamica,
                caudal: this.caudal,
                diametroDeSuccion: this.diametroDeSuccion,
                diametroDeDescarga: this.diametroDeDescarga,
                rodamientos: this.rodamientos,
                
            };

            axios.post('http://localhost:8080/api/bombas', bomba)
                .then(response => {
                    console.log('bomba guardada:', response.data);
                    alert('Bomba guardada exitosamente');
                    this.Id = '';
                    this.nombre = ''; 
                    this.marca = '';
                    this.alturaDinamica = '';
                    this.caudal = '';
                    this.diametroDeSuccion = '';
                    this.diametroDeDescarga = '';
                    this.$emit('actualizar-tabla');  
                   
                })
                .catch(error => {
                    console.error('Error al guardar la bomba:', error);
                    alert('Error al guardar la bomba');
                    
                });
        },
        consultar() {
            axios.get('http://localhost:8080/api/bombas/' + this.Id)
                .then(response => {
                    console.log('bombas consultadas:', response.data);
                    this.Id = response.data.id || this.Id;
                    this.nombre = response.data.nombre;
                    this.marca = response.data.marca;
                    this.alturaDinamica = response.data.alturaDinamica;
                    this.caudal = response.data.caudal;
                    this.diametroDeSuccion = response.data.diametroDeSuccion;
                    this.diametroDeDescarga = response.data.diametroDeDescarga;
                })
                .catch(error => {
                    console.error('Error al consultar las bombas:', error);
                    alert('Error al consultar las bombas');
                    
                });
        },
        actualizar() {
            const bomba = {
                id: this.Id,
                nombre: this.nombre,
                marca: this.marca,
                alturaDinamica: this.alturaDinamica,
                caudal: this.caudal,
                diametroDeSuccion: this.diametroDeSuccion,
                diametroDeDescarga: this.diametroDeDescarga,
            };

            axios.put('http://localhost:8080/api/bombas/actualizar/' + this.Id, bomba)
                .then(response => {
                    console.log('Bomba actualizada:', response.data);
                    alert('Bomba actualizada exitosamente');
                    this.$emit('actualizar-tabla');
                })
                .catch(error => {
                    console.error('Error al actualizar la bomba:', error);
                    alert('Error al actualizar la bomba');
                });
        },
        eliminar() {
            axios.delete('http://localhost:8080/api/bombas/' + this.Id)
                .then(response => {
                    console.log('Bomba eliminada:', response.data);
                    alert('Bomba eliminada exitosamente');
                    this.Id = '';
                    this.nombre = ''; 
                    this.marca = '';
                    this.alturaDinamica = '';
                    this.caudal = '';
                    this.diametroDeSuccion = '';
                    this.diametroDeDescarga = '';
                    this.$emit('actualizar-tabla');
                    
                })
                .catch(error => {
                    console.error('Error al eliminar la bomba:', error);
                    alert('Error al eliminar la bomba');
                    
                });
        }
    }
}

</script>