<template>
    <div>
        <h1>Lista de Publicaciónes</h1>
        <h1 v-if="cargando">Cargando...</h1>
        
        <table class="table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>TITULO</th>
                    <th>COMPLETADO</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="dato in lista_datos" :key="dato.id">
                    <td>{{ dato.id }}</td>
                    <td>{{ dato.title }}</td>
                    <td>{{ dato.completed }}</td>
                </tr>
            </tbody>

        </table>
        

    </div>
</template>

<script>
import axios from 'axios'

export default {
    data(){
        return {
            lista_datos: [],
            cargando: true
        }
    },
    mounted(){
        axios.get("https://jsonplaceholder.typicode.com/todos/")
            .then((datos) => {
                console.log("****************");
                console.log(datos.data[2].title)
                this.lista_datos = datos.data;
                console.log("****************");
                this.cargando = false
            });
    },


}
</script>

<style>

</style>