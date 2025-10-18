<template>
  <section>
    <h2>Muro</h2>

    <form class="new-post-form" @submit.prevent="addPost">
      <textarea v-model="newText" placeholder="Escribe algo..." required></textarea>
      <input type="file" @change="onFileChange" accept="image/*" />
      <button type="submit">Compartir</button>
    </form>

    <div id="postsContainer">
      <div v-for="(post, i) in posts" :key="i" class="post">
        <strong>{{ post.autor }}</strong> - {{ post.titulo }}
        <p>{{ post.fecha }}</p>
        <p>{{ post.texto }}</p>
        <img v-if="post.imagen" :src="post.imagen" alt="imagen del post" />
        <div class="actions">
          <button>👍 Me gusta</button>
          <button>🔁 Compartir</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const posts = ref([
  { autor: 'Karina', titulo: 'Nueva pintura', fecha: 'Lunes 11:46 am', texto: '', imagen: '/img/descarga (13).jpg' },
  { autor: 'Pedro', titulo: 'Vacaciones', fecha: 'Martes 9:15 am', texto: '', imagen: '/img/descarga (11).jpg' },
  { autor: 'Juan', titulo: 'Nueva receta', fecha: 'Martes 1:30 am', texto: '', imagen: '/img/descarga (12).jpg' },
])

const newText = ref('')
const newImage = ref(null)

function onFileChange(e) {
  const file = e.target.files[0]
  if (!file) return
  const reader = new FileReader()
  reader.onload = () => {
    newImage.value = reader.result
  }
  reader.readAsDataURL(file)
}

function addPost() {
  if (!newText.value && !newImage.value) return
  posts.value.unshift({
    autor: 'Tú',
    titulo: 'Nueva publicación',
    fecha: new Date().toLocaleString(),
    texto: newText.value,
    imagen: newImage.value
  })
  newText.value = ''
  newImage.value = null
}
</script>
