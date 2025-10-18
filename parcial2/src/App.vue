<template>
  <header class="topbar">
    <div class="logo">facebook</div>
    <input type="search" class="search" placeholder="Buscar" />
  </header>

  <nav class="tabs">
    <button
      v-for="tab in tabs"
      :key="tab"
      :class="['tab', { active: activeTab === tab }]"
      @click="activeTab = tab"
    >
      {{ tab }}
    </button>
  </nav>

  <main class="layout">
    <aside class="sidebar">
      <section class="profile">
        <img src="/img/descarga (5).jpg" alt="Foto de perfil" class="avatar" />
        <h2 class="username">Karina</h2>

        <div class="links">
          <p><strong>Información</strong></p>
          <p>Info</p>

          <p><strong>Amigos</strong></p>
          <div class="friends">
            <img src="/img/descarga (6).jpg" alt="Amigo 1" />
            <img src="/img/mamaco.jpg" alt="Amigo 2" />
            <img src="/img/perrito.jpg" alt="Amigo 3" />
            <img src="/img/descarga (8).jpg" alt="Amigo 4" />
            <img src="/img/descarga (9).jpg" alt="Amigo 5" />
            <img src="/img/descarga (10).jpg" alt="Amigo 6" />
          </div>
          <a href="#">Ver todo</a>
        </div>
      </section>
    </aside>

    <section class="content">
      <component :is="currentView" />
    </section>
  </main>

  <footer class="footer">
    <p>&copy; 2025 Facebook </p>
  </footer>
</template>

<script setup>
import { ref, computed } from 'vue'
import Muro from './components/Muro.vue'
import Info from './components/Info.vue'
import Fotos from './components/Fotos.vue'
import Cajas from './components/Cajas.vue'

const tabs = ['Muro', 'Info', 'Fotos', 'Cajas']
const activeTab = ref('Muro')

const currentView = computed(() => {
  switch (activeTab.value) {
    case 'Info': return Info
    case 'Fotos': return Fotos
    case 'Cajas': return Cajas
    default: return Muro
  }
})
</script>

<style scoped>
@import './assets/styles.css';
</style>
