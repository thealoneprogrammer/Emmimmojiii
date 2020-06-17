<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <Search v-on:search-emoji="searchEmoji" />
      <Emojis v-for="emoji in emojis" :emoji="emoji" :key="emoji.slug" />
    </v-flex>
  </v-layout>
</template>

<script>
import Search from '../components/Search'
import Emojis from '../components/Emojis'
import axios from 'axios'

export default {
  data() {
    return {
      emojis: []
    }
  },
  async created() {
    const _apiKey = process.env.emoji_api_key
    const config = {
      headers: {
        accept: 'application/json'
      }
    }
    try {
      const response = await axios.get(
        `https://emoji-api.com/emojis?access_key=${_apiKey}`,
        config
      )

      this.emojis = response.data
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    async searchEmoji(query) {
      this.$nuxt.$loading.start()
      const _apiKey = process.env.emoji_api_key
      const config = {
        headers: {
          accept: 'application/json'
        }
      }
      try {
        const response = await axios.get(
          `https://emoji-api.com/emojis?search=${query}` +
            `&access_key=${_apiKey}`,
          config
        )

        this.emojis = response.data
        this.$nuxt.$loading.finish()
      } catch (error) {
        console.log(error)
      }
    }
  },
  head: () => {
    return {
      title: 'Emoji App'
    }
  },
  components: {
    Search,
    Emojis
  }
}
</script>
