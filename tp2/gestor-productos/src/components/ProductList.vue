<template>
  <div>
    <h3>Lista de Productos:</h3>

    <div v-if="props.productos.length === 0">
      No hay productos en esta categoría.
    </div>

    <ul>
      <ProductItem
        v-for="producto in props.productos"
        :key="producto.id"
        :producto="producto"
        @eliminar="eliminar"
      />
    </ul>
  </div>
</template>


<script setup>
import { reactive } from 'vue'
import ProductItem from './ProductItem.vue'


const props = defineProps({
  productos: Array
})

const emit = defineEmits(['eliminar'])


function eliminar(id) {
  emit('eliminar', id)
}
</script>

<style scoped>
h3 {
  margin-top: 10px;
  text-align: left;
  text-decoration: underline;
  color: rgb(45, 45, 184);
}


</style>