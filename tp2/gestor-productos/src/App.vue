<template>
  
    <h1>Gestor de Productos</h1>

    <ProductForm @crear="crearProducto" />

    <hr class="linea"/>
    
    <div class="contenido">
      <div class="filtro">
        <h3>Filtro</h3>
          <select v-model="filtro">
              <option value="todos">Todos</option>
              <option value="electronica">Electrónica</option>
              <option value="libreria"  >Librería</option>
              <option value="hogar">Hogar</option>
              <option value="ropa">Ropa</option>
              <option value="alimentos">Alimentos</option>
          </select>
      </div>
    
      <div class="listado">
        <ProductList
          :productos="productosFiltrados"
          @eliminar="eliminarProducto" />
      </div>
    </div>

    <hr class="linea2"/>
    
      <div class="centrado">
        <h3 class="Resumen">Resumen</h3>
          <p>Total de productos: {{ totalProductos }}</p>
          <p>Valor del inventario: ${{ valorInventario }}</p>
      </div>
      
</template>


<script setup>
import { ref, computed } from 'vue'
import ProductForm from './components/ProductForm.vue'
import ProductList from './components/ProductList.vue'


const productos = ref([])
const filtro = ref('todos')
let nextId = 1


function crearProducto(producto) {
  producto.id = nextId++
  productos.value.push(producto)
}

function eliminarProducto(id) {
  productos.value = productos.value.filter(p => p.id !== id)
}


const productosFiltrados = computed(() => {
  if (filtro.value === 'todos') return productos.value
  return productos.value.filter(p => p.categoria === filtro.value)
})

const totalProductos = computed(() => productos.value.length)

const valorInventario = computed(() =>
  productos.value.reduce((acc, p) => acc + (p.precio * p.stock), 0)
)
</script>





<style>
body {
  font-family: Arial, sans-serif;
  background-color: #eee;
  margin: 0;
}
h1{
  text-align: center;
  text-decoration: underline;
  color: rgb(45, 45, 184);
}
.linea {
  border: 1px solid rgb(45, 45, 184);
}
.linea2 {
  border: 3px solid rgb(45, 45, 184);
}
#app {
  padding: 20px;
}

.contenido {
  display: flex;
  gap: 20px;
  margin-top: 20px;
}

.listado {
  flex: 1;
}
.Resumen {
  text-align: center;
  text-decoration: underline;
  color: rgb(45, 45, 184);
}
.centrado {
  text-align: center;
}

.filtro {
  width: 220px;
  background-color: white;
  padding: 15px;
  border-radius: 10px;
  height: fit-content;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.filtro h3 {
  margin-top: 0;
  text-align: center;
  color: rgb(45, 45, 184);
}

.filtro select {
  width: 100%;
  padding: 8px;
  border-radius: 6px;
  border: 1px solid #ccc;
  margin-top: 10px;
}


</style>