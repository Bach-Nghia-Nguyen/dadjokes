<template>
  <nuxt-link :to="'Jokes/' + id">
    <div class="joke">
      <p>{{ joke }}</p>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: 'Joke',
  props: {
    joke: {
      type: String,
      default: '',
    },
    id: {
      type: String,
      default: '',
    },
  },
}
</script>

<style>
.joke {
  padding: 1rem;
  border: 1px dashed #ccc;
  margin: 1rem 0;
}
</style>
