<template>
  <ListaProductos :productos="perifericos" />
</template>

<script setup>
import { onMounted, onUnmounted, onActivated, onDeactivated } from 'vue'
import { productos } from '../../data/productos.js'
import ListaProductos from '../ListaProductos.vue'


const perifericos = productos.filter(p => p.categoria === 'Periféricos')

onMounted(()     => console.log('TabPerifericos — montado'))
onUnmounted(()   => console.log('TabPerifericos — desmontado'))
onActivated(()   => console.log('TabPerifericos — activado'))
onDeactivated(() => console.log('TabPerifericos — desactivado'))
</script>
