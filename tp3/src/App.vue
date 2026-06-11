<template>
  <div class="app">
    <header class="app__header">
      <h1>Catálogo de Productos</h1>
      
    </header>

    <main class="app__main">
      
      <section class="seccion">
        <h2 class="seccion__titulo">Parte 1 — Slots en TarjetaProducto</h2>
        

        <div class="demo-grid">

          <div>
            <p class="demo-label">Instancia 1 — tres slots provistos</p>
            <TarjetaProducto>
              <template #header>
                <div class="prod__nombre">Notebook Lenovo IdeaPad</div>
                <span class="prod__categoria">Electrónica</span>
              </template>

              <template #body="{ expandida, toggleExpandir }">
                <div class="prod__precio">$ 850.000</div>
                <button class="btn-toggle" @click="toggleExpandir">
                  {{ expandida ? 'Ocultar ' : 'Ver detalle ' }}
                </button>
                <div v-if="expandida" class="prod__detalle">Stock: 12 unidades</div>
              </template>

              <template #footer>
                <button class="btn-accion">Agregar al carrito</button>
              </template>
            </TarjetaProducto>
          </div>

          <div>
            <p class="demo-label">Instancia 2 — sin <code>#footer</code> (fallback activo)</p>
            <TarjetaProducto>
              <template #header>
                <div class="prod__nombre">Mouse inalámbrico Logitech</div>
                <span class="prod__categoria">Periféricos</span>
              </template>

              <template #body="{ expandida, toggleExpandir }">
                <div class="prod__precio">$ 48.000</div>
                <button class="btn-toggle" @click="toggleExpandir">
                  {{ expandida ? 'Ocultar ' : 'Ver detalle ' }}
                </button>
                <div v-if="expandida" class="prod__detalle">Stock: 30 unidades</div>
              </template>
            </TarjetaProducto>
          </div>

          <div>
            <p class="demo-label">Instancia 3 — libre (producto destacado)</p>
            <TarjetaProducto>
              <template #header>
                <div class="prod__nombre">Auriculares Sony WH-1000</div>
                <span class="prod__categoria">Audio</span>
              </template>

              <template #body="{ expandida, toggleExpandir }">
                <div class="prod__precio">$ 310.000</div>
                <div class="prod__rating">Producto Destacado </div>
                <button class="btn-toggle" @click="toggleExpandir">
                  {{ expandida ? 'Ocultar ' : 'Especificaciones ' }}
                </button>
                <div v-if="expandida" class="prod__detalle">
                  Noise Cancelling · 30hs batería · Bluetooth 5.2
                </div>
              </template>

              <template #footer>
                <div style="display:flex; gap:8px">
                  <button class="btn-accion">Comprar</button>
                  <button class="btn-toggle">♡ Guardar</button>
                </div>
              </template>
            </TarjetaProducto>
          </div>

        </div>
      </section>

      <section class="seccion">
        <h2 class="seccion__titulo">Partes 2 y 3 — ListaProductos + Tabs dinámicos</h2>
        
        <PanelPestanas />
      </section>

    </main>
  </div>
</template>

<script setup>
import TarjetaProducto from './components/TarjetaProducto.vue'
import PanelPestanas from './PanelPestanas.vue'
</script>

<style>
/* ── Variables globales ── */
:root {
  --bg: #d2e4f4;
  --card-bg: #ffffff;
  --footer-bg: #fafaf9;
  --border: #e5e5e2;
  --accent: #3b6ef5;
  --accent-soft: #eff3fe;
  --text: #1a1a1a;
  --text-muted: #8a8a8a;
  --font: 'DM Sans', 'Segoe UI', sans-serif;
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: var(--font);
  background: var(--bg);
  color: var(--text);
  line-height: 1.5;
}


.app {
  max-width: 1100px;
  margin: 0 auto;
  padding: 32px 20px 60px;
}

.app__header {
  margin-bottom: 40px;
}

.app__header h1 {
  font-size: 1.8rem;
  font-weight: 700;
  letter-spacing: -0.03em;
  color: var(--text);
}



.seccion {
  margin-bottom: 48px;
}

.seccion__titulo {
  font-size: 1.05rem;
  font-weight: 600;
  margin-bottom: 6px;
}


.demo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 20px;
}

.demo-label {
  font-size: 0.78rem;
  color: var(--text-muted);
  margin-bottom: 8px;
}

.demo-label code {
  background: #efefef;
  padding: 1px 5px;
  border-radius: 4px;
}


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
  font-size: 0.82rem;
  color: var(--text-muted);
}

.prod__rating {
  color: #e4ad16;
  font-size: 0.82rem;
  margin-bottom: 8px;
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
