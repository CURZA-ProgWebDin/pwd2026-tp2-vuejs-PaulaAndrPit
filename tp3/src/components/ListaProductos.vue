<template>
  <div>
   
    <div v-if="cargando" class="lista__cargando">
      <span class="spinner" /> Cargando...
    </div>

    
    <div v-else ref="box" class="lista">
      <TarjetaProducto v-for="p in productos" :key="p.id">

        
        <template #header>
          <div class="prod__nombre">{{ p.nombre }}</div>
          <span class="prod__categoria">{{ p.categoria }}</span>
        </template>

        
        <template #body="{ expandida, toggleExpandir }">
          <div class="prod__precio">$ {{ p.precio.toLocaleString('es-AR') }}</div>

          <button class="btn-toggle" @click="toggleExpandir">
            {{ expandida ? 'Ocultar detalle ' : 'Ver detalle ' }}
          </button>

          <div v-if="expandida" class="prod__detalle">
            <span class="prod__stock" :class="{ 'stock--bajo': p.stock < 10 }">
              Stock: {{ p.stock }} unidades
            </span>
          </div>
        </template>

        
        <template #footer>
          <button class="btn-accion">Agregar al carrito</button>
        </template>

      </TarjetaProducto>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUpdated, onBeforeUnmount, useTemplateRef } from 'vue'
import TarjetaProducto from './TarjetaProducto.vue'

const props = defineProps({
  productos: {
    type: Array,
    required: true
  }
})


const box = useTemplateRef('box')

const cargando = ref(false)
let timer = null


function esperar(ms) {
  return new Promise(resolve => setTimeout(resolve, ms))
}


async function cargarProductos() {
  cargando.value = true
  await esperar(800)
  cargando.value = false
}

onMounted(() => {
  
  cargarProductos()

  
  timer = setInterval(() => {
    cargarProductos()
  }, 30000)
})

onUpdated(() => {
  
  if (box.value) {
    box.value.scrollTop = box.value.scrollHeight
  }
})

onBeforeUnmount(() => {
  
  clearInterval(timer)
  console.log('ListaProductos desmontado — polling detenido')
})
</script>

<style scoped>
.lista__cargando {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 24px;
  color: var(--text-muted);
  font-size: 0.9rem;
}

.spinner {
  display: inline-block;
  width: 16px;
  height: 16px;
  border: 2px solid var(--border);
  border-top-color: var(--accent);
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.lista {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 14px;
  max-height: 520px;
  overflow-y: auto;
  padding: 4px 2px;
}


.lista::-webkit-scrollbar { width: 6px; }
.lista::-webkit-scrollbar-track { background: transparent; }
.lista::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }

.prod__nombre {
  font-weight: 600;
  font-size: 0.92rem;
  color: var(--text);
  margin-bottom: 4px;
  line-height: 1.3;
}

.prod__categoria {
  font-size: 0.72rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--accent);
  background: var(--accent-soft);
  padding: 2px 7px;
  border-radius: 20px;
}

.prod__precio {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 8px;
}

.prod__detalle {
  margin-top: 8px;
}

.prod__stock {
  font-size: 0.82rem;
  color: var(--text-muted);
}

.stock--bajo {
  color: #e05252;
  font-weight: 600;
}

.btn-toggle {
  font-size: 0.78rem;
  background: none;
  border: 1px solid var(--border);
  border-radius: 5px;
  padding: 3px 10px;
  cursor: pointer;
  color: var(--text-muted);
  transition: border-color 0.15s, color 0.15s;
}

.btn-toggle:hover {
  border-color: var(--accent);
  color: var(--accent);
}

.btn-accion {
  font-size: 0.8rem;
  background: var(--accent);
  color: #fff;
  border: none;
  border-radius: 6px;
  padding: 5px 14px;
  cursor: pointer;
  transition: opacity 0.15s;
}

.btn-accion:hover {
  opacity: 0.85;
}
</style>
