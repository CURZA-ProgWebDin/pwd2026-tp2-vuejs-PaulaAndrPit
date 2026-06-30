<template>
  <form @submit.prevent="manejarSubmit">

    <h3>Agregar producto</h3>
      
      <label for="nombre">Nombre del producto:</label>
      <input v-model="nombre" placeholder="Producto" />
      
      <label for="precio">Precio:</label>
      <input v-model="precio" placeholder="$" />
      
      <label for="stock">Stock:</label>
      <input v-model="stock" placeholder="Cantidad" />
      
      <label for="categoria">Categoría:</label>
        <select v-model="categoria" >
          <option disabled value="">Seleccionar categoría</option>
          <option value="electronica">Electrónica</option>
          <option value="libreria"  >Librería</option>
          <option value="hogar">Hogar</option>
          <option value="ropa">Ropa</option>
          <option value="alimentos">Alimentos</option>
        </select>

      <button type="submit" class="boton">AGREGAR</button>
  
  </form>

</template>



<script setup>
import { ref } from 'vue'

const emit = defineEmits(['crear'])

const nombre = ref('')
const precio = ref('')
const stock = ref('')
const categoria = ref('')

function LimpiarForm() {
  nombre.value = ''
  precio.value = ''
  stock.value = ''
  categoria.value = ''
}


function manejarSubmit() {

  if (!nombre.value || !precio.value || !stock.value || !categoria.value) {
    alert('Todos los campos son obligatorios')
    return
  }

  if ((precio.value < 0) || isNaN(precio.value) || (stock.value < 0) || isNaN(stock.value)) {
    alert('Precio y/o stock deben ser números positivos')
    return
  }

  const producto = {
    nombre: nombre.value,
    precio: Number(precio.value),
    stock: Number(stock.value),
    categoria: categoria.value
  }

  emit('crear', producto)
  LimpiarForm()
  
}
</script>



<style scoped>
form {
  max-width: 400px;
  margin: 30px auto;
  padding: 20px;
  border-radius: 10px;
  background-color: #f5f5f5;
}

h3 {
  text-align: center;
  margin-bottom: 10px;
  color:rgb(45, 45, 184)
}

label {
  display: block;
  margin-top: 10px;
  font-weight: bold;
}

input, select {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  border-radius: 6px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

input:focus, select:focus {
  outline: none;
  border-color: rgb(45, 45, 184);
}

.boton {
  display: block;
  margin: 20px auto 0 auto;
  background-color: rgb(45, 45, 184);
  color: white;
  border: none;
  border-radius: 10px;
  padding: 12px 25px;
  font-size: 16px;
  cursor: pointer;
}

.boton:hover {
  background-color: rgb(3, 3, 83);
}
</style>