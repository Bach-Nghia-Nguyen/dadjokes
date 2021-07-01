<template>
  <div>
    <SearchJokes @search-text="searchText" />

    <Joke
      v-for="joke in jokes"
      :id="joke.id"
      :key="joke.id"
      :joke="joke.joke"
    />

    <p v-if="!jokes || jokes.length === 0">There is no joke</p>
  </div>
</template>

<script>
import axios from 'axios'
import Joke from '../../components/Joke.vue'
import SearchJokes from '../../components/SearchJokes.vue'

export default {
  components: {
    Joke,
    SearchJokes,
  },
  data() {
    return {
      jokes: [],
    }
  },

  head() {
    return {
      title: 'Dad Jokes',
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
      const res = await axios.get('https://icanhazdadjoke.com/search', config)
      console.log('Joke list:', res.data.results[15])

      this.jokes = res.data.results
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: 'application/json',
        },
      }

      try {
        const res = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}`,
          config
        )

        this.jokes = res.data.results
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>

<style></style>
