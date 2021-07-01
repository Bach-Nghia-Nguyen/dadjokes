<template>
  <div>
    <nuxt-link to="/Jokes">Back to Jokes</nuxt-link>
    <h2>{{ joke }}</h2>
    <hr />
    <small>Joke ID: {{ $route.params.id }}</small>
    <button @click="nextJoke">Next Joke</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      joke: '',
    }
  },
  head() {
    return {
      title: this.joke,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Best place for corny dad jokes',
        },
      ],
    }
  },
  async created() {
    const config = {
      headers: {
        Accept: 'application/json',
      },
    }

    try {
      const res = await axios.get(
        `https://icanhazdadjoke.com/j/${this.$route.params.id}`,
        config
      )
      this.joke = res.data.joke
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    nextJoke() {
      this.$emit('next-joke', this.$route.params.id)
      console.log('current joke id:', this.$route.params.id)
    },
  },
}
</script>

<style></style>
