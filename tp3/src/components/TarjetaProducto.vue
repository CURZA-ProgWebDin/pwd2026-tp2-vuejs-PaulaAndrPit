<template>
  <div class="tarjeta" :class="{ 'tarjeta--expandida': expandida }">
    <div class="tarjeta__header">
      <slot name="header" />
    </div>

    <div class="tarjeta__body">
      <slot name="body" :expandida="expandida" :toggleExpandir="toggleExpandir" />
    </div>

    <div class="tarjeta__footer">
      <slot name="footer">
        <span class="tarjeta__fallback">Sin acciones disponibles</span>
      </slot>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'


const expandida = ref(false)

function toggleExpandir() {
  expandida.value = !expandida.value
}
</script>

<style scoped>
.tarjeta {
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 10px;
  overflow: hidden;
  transition: box-shadow 0.2s, transform 0.2s;
}

.tarjeta:hover {
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
  transform: translateY(-2px);
}

.tarjeta--expandida {
  border-color: var(--accent);
}

.tarjeta__header {
  padding: 14px 16px 10px;
  border-bottom: 1px solid var(--border);
}

.tarjeta__body {
  padding: 12px 16px;
}

.tarjeta__footer {
  padding: 10px 16px 14px;
  border-top: 1px solid var(--border);
  background: var(--footer-bg);
}

.tarjeta__fallback {
  font-size: 0.78rem;
  color: var(--text-muted);
  font-style: italic;
}
</style>
