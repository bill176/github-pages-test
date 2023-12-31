<script setup lang="ts">
import { onMounted, ref } from 'vue';


type Post = {
  userId: number,
  id: number,
  title: string,
  body: string
}

defineProps<{
  msg: string
}>()

const emptyPost: Post = { userId:0, id:0, title:'', body:'' }

let body = ref<Post>(emptyPost)

onMounted(async () => {
  await new Promise(r => setTimeout(r, 2000));
  const response = await fetch('https://jsonplaceholder.typicode.com/posts/1')
  body.value = await response.json()
})
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
    </h3>
    <div v-if="body.userId !== 0">
      <h3>Here is a post for you:</h3>
      <h3>{{ body.title }}</h3>
      <h3>{{ body.body }}</h3>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
