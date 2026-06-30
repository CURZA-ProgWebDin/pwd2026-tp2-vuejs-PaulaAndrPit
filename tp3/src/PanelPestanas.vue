<!--
  PanelPestanas.vue
  Muestra dos versiones del panel de pestañas:
  - Sin KeepAlive: cada cambio de pestaña destruye el componente anterior (onUnmounted) y crea el nuevo (onMounted)
  - Con KeepAlive: los componentes se cachean; al cambiar se ejecuta onDeactivated/onActivated en lugar de destruir/crear

  ¿Cuándo conviene usar KeepAlive?
  - Conviene usarlo cuando el componente tiene estado local costoso de reconstruir (formularios a medio completar,
    listas con scroll, datos ya cargados desde una API) y queremos conservarlo al volver a la pestaña.
    También cuando la carga inicial es cara (fetch, procesamiento) y queremos evitar repetirla.

  - NO conviene usarlo cuando los datos deben estar siempre frescos al entrar (un feed en tiempo real,
    un dashboard que requiere datos actualizados), o cuando los componentes consumen mucha memoria y
    mantenerlos todos vivos en segundo plano es más costoso que recrearlos.
-->

<template>
  <div class="panel">


    <div class="panel__tabs">
      <button
        v-for="tab in tabs"
        :key="tab.key"
        class="panel__tab-btn"
        :class="{ 'panel__tab-btn--activo': tabActiva === tab.componente }"
        @click="tabActiva = tab.componente"
      >
        {{ tab.label }}
      </button>
    </div>

    <div class="panel__grid">


      <div class="panel__seccion">
        <div class="panel__seccion-titulo">
          <span class="badge badge--sin">Sin KeepAlive</span>
          <span class="panel__hint">onMounted / onUnmounted en cada cambio</span>
        </div>
        <component :is="tabActiva" />
      </div>


      <div class="panel__seccion">
        <div class="panel__seccion-titulo">
          <span class="badge badge--con">Con KeepAlive</span>
          <span class="panel__hint">onActivated / onDeactivated — el estado se preserva</span>
        </div>
        <KeepAlive>
          <component :is="tabActiva" />
        </KeepAlive>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, shallowRef } from 'vue'
import TabTodos from './components/tabs/TabTodos.vue'
import TabElectronica from './components/tabs/TabElectronica.vue'
import TabPerifericos from './components/tabs/TabPerifericos.vue'

const tabs = [
  { key: 'todos',       label: 'Todos',       componente: TabTodos       },
  { key: 'electronica', label: 'Electrónica', componente: TabElectronica },
  { key: 'perifericos', label: 'Periféricos', componente: TabPerifericos },
]


const tabActiva = shallowRef(TabTodos)
</script>

<style scoped>
.panel {
  width: 100%;
}

.panel__tabs {
  display: flex;
  gap: 6px;
  margin-bottom: 20px;
}

.panel__tab-btn {
  padding: 7px 18px;
  border-radius: 7px;
  border: 1px solid var(--border);
  background: transparent;
  cursor: pointer;
  font-size: 0.88rem;
  color: var(--text-muted);
  transition: all 0.15s;
}

.panel__tab-btn:hover {
  border-color: var(--accent);
  color: var(--accent);
}

.panel__tab-btn--activo {
  background: var(--accent);
  border-color: var(--accent);
  color: #fff;
}

.panel__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

@media (max-width: 700px) {
  .panel__grid { grid-template-columns: 1fr; }
}

.panel__seccion {
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 16px;
}

.panel__seccion-titulo {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 14px;
}

.badge {
  font-size: 0.75rem;
  font-weight: 600;
  padding: 3px 10px;
  border-radius: 20px;
  letter-spacing: 0.03em;
}

.badge--sin {
  background: #fee9e2;
  color: #b9431c;
}

.badge--con {
  background: #f2d1fa;
  color: #52065f;
}

.panel__hint {
  font-size: 0.75rem;
  color: var(--text-muted);
}
</style>
