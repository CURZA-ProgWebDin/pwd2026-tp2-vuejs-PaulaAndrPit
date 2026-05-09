<template>
  
  <li>
    <div class="item">
      <strong>{{ producto.nombre }}: </strong>
              Precio: {{ producto.precio }}
              Stock: {{ producto.stock }}
              Categoría: {{ producto.categoria }}
  

      <button @click="eliminar" class="boton2">Eliminar</button>
    </div>
  </li>
  
</template>


<script setup>
const props = defineProps({
  producto: Object
})

const emit = defineEmits(['eliminar'])

function eliminar() {
  emit('eliminar', props.producto.id)
}
</script>



<style scoped>

.boton2 {
  background-color: rgb(45, 45, 184);
  color: white;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
}
.boton2:hover {
  background-color: rgb(3, 3, 83);
}

.item strong {
  font-size: 18px;
  text-transform: uppercase;
}
</style>




