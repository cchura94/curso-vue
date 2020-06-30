<template>
    <div>
        <h1>{{ titulo }}</h1>
        <!--p>{{ prod }}</p-->
        <!--p>{{ productos }}</p-->
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <h2>Lista de Productos</h2>
                    <button class="btn btn-primary" v-on:click="estado = !estado"> {{ (estado)?'NUEVO PRODUCTO':'LISTAR PRODUCTOS' }} </button>
                    <table class="table" v-if="estado">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>NOMBRE</th>
                                <th>CANTIDAD</th>
                                <th>PRECIO</th>
                                <th>DETALLE</th>
                                <th>ACCIONES</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(p, index) in productos" :key="index">
                                <td>{{ index + 1 }}</td>
                                <td>{{ p.nombre }}</td>
                                <td>{{ p.cantidad }}</td>
                                <td>{{ p.precio }}</td>
                                <td>{{ p.detalle }}</td>
                                <td>
                                    <button v-on:click="add_carrito(p)" class="btn btn-success">Añadir al carrito</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>

                    <div class="row" v-if="!estado">
                        <div class="col-md-12">
                            <h2>Nuevo Producto</h2>
                            
                            <label for="">Nombre:</label>
                            <input type="text" v-model="producto.nombre" class="form-control">
                            <label for="">Cantidad:</label>
                            <input type="number" v-model="producto.cantidad" class="form-control">
                            <label for="">Precio:</label>
                            <input type="text" v-model="producto.precio" class="form-control">
                            <label for="">Detalle:</label>
                            <textarea v-model="producto.detalle" class="form-control"></textarea>

                            <button class="btn btn-success" v-on:click="add_nuevoProducto()">Guardar Nuevo Producto</button>
                            {{ producto }}
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <h2>Carrito de compras</h2>
                    <table class="table">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>NOMBRE</th>
                                <th>CANTIDAD</th>
                                <th>PRECIO</th>
                                <th>SUB-TOTAL</th>
                                <th>ACCIONES</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(p, index) in carrito" :key="index">
                                <td>{{ index + 1 }}</td>
                                <td>{{ p.nombre }}</td>
                                <td><input type="text" v-model="p.cantidad"> </td>
                                <td>{{ p.precio }}</td>
                                <td>{{ p.subtotal }}</td>
                                <td>
                                    <button v-on:click="eliminar(index)" class="btn btn-danger">eliminar</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>

            </div>
        </div>
        
    
    </div>  
</template>

<script>
import Swal from 'sweetalert2'

export default {
    data() {
        return {
            titulo: "Carrito de Ventas",
            prod: {nombre: "Laptop", cantidad: 12, precio: 6700, detalle: "detalle" },
            productos: [],
            carrito: [],
            estado: true,
            producto: {
                nombre: "",
                cantidad: 1,
                precio: 0.00,
                detalle: ""
            }
        }
    },
    created(){
        

        this.productos.push(this.prod) 
        this.productos.push({
            nombre: "Televisor",
            cantidad: 16,
            precio: 3500,
            detalle: "Televisor marca ABC"
        }) 
         
    },
    mounted(){
    },
    methods: {
        add_carrito(p){
           /*const { value: email } = Swal.fire({
            title: 'Ingrese cantidad',
            input: 'email',
            inputPlaceholder: 'Enter your email address'
            })

            if (email) {
            Swal.fire(`Entered email: ${email}`)
            }*/

            var cant = prompt("Ingrese la cantidad:")

            this.carrito.push({
                nombre: p.nombre,
                cantidad: cant,
                precio: p.precio,
                subtotal: cant * p.precio
            })
            Swal.fire({
                title: 'Correcto!',
                text: 'Producto agregado al carrito',
                icon: 'success',
                confirmButtonText: 'Aceptar'
            })  

            //console.log("Agregando al carrito", p)
        },
        eliminar(i){

            const swalWithBootstrapButtons = Swal.mixin({
            customClass: {
                confirmButton: 'btn btn-success',
                cancelButton: 'btn btn-danger'
            },
            buttonsStyling: false
            })

            swalWithBootstrapButtons.fire({
            title: 'Estás seguro de eliminar?',
            text: "Si eliminas no podrás recuperar",
            icon: 'warning',
            showCancelButton: true,
            confirmButtonText: 'Si, Eliminar!',
            cancelButtonText: 'No, cancelar!',
            reverseButtons: true
            }).then((result) => {
            if (result.value) {
                this.carrito.splice(i, 1);
                swalWithBootstrapButtons.fire(
                'Eliminado!',
                'Tu Producto del carrito ha sido eliminado.',
                'success'
                )
            } else if (
                /* Read more about handling dismissals below */
                result.dismiss === Swal.DismissReason.cancel
            ) {
                swalWithBootstrapButtons.fire(
                'Cancelado',
                'prueba :)',
                'error'
                )
            }
            })

            
        },

        add_nuevoProducto(){
            this.productos.push(this.producto);
            this.estado = true;

            Swal.fire({
                title: 'Correcto!',
                text: 'Producto registrado correctamente',
                icon: 'success',
                confirmButtonText: 'Aceptar'
            }) 
        }
    }


}
</script>

<style>

</style>