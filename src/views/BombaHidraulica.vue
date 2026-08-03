<template>

    <div class="bombas">

        <div class="components">

            <FormularioBombaHidraulica @actualizar-tabla="actualizarTabla"/>
            <TablaBombaHidraulica ref="tablaBombaHidraulica"/>

        </div>

    </div>

</template>

<script>

import FormularioBombaHidraulica from '@/components/FormularioBombaHidraulica.vue';
import TablaBombaHidraulica from '@/components/TablaBombaHidraulica.vue';

export default {

    name: "BombaHidraulicaView",

    components: {
        FormularioBombaHidraulica,
        TablaBombaHidraulica
    },
    methods: {
        actualizarTabla() {
            this.$refs.tablaBombaHidraulica.obtenerBombasHidraulicas();
        }
    }

}

</script>

<style>
/* ===== ESTILOS GENERALES ===== */

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body{
    background: #f2f2f2;
    font-family: Arial, Helvetica, sans-serif;
}

/* ===== CONTENEDOR PRINCIPAL ===== */

.bomba{
    width: 100%;
    padding: 20px;
}

.components{
    display: flex;
    gap: 20px;
    justify-content: center;
    align-items: flex-start;
}

/* ===== TARJETAS ===== */

.container{
    background: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0px 2px 8px rgba(0,0,0,0.2);
}

/* ===== FORMULARIO ===== */

.container h1{
    text-align: center;
    margin-bottom: 30px;
    color: #333;
}

#student-form{
    width: 350px;
}

.form-group{
    margin-bottom: 20px;
}

.form-group label{
    display: block;
    margin-bottom: 8px;
    font-weight: bold;
    color: #555;
    text-align: center;
}

.form-group input{
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 3px;
    outline: none;
}

.form-group input:focus{
    border-color: #1e90ff;
}

/* ===== BOTONES ===== */

button{
    width: 100%;
    padding: 10px;
    margin-top: 10px;
    border: none;
    background: #1e90ff;
    color: white;
    border-radius: 3px;
    cursor: pointer;
    font-size: 14px;
    transition: 0.3s;
}

button:hover{
    background: #0d6efd;
}

/* ===== TABLA ===== */

table{
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
}

thead{
    background: #1e90ff;
    color: white;
}

th,
td{
    border: 1px solid #999;
    padding: 12px;
    text-align: left;
}

tbody tr:nth-child(even){
    background: #f9f9f9;
}
</style>