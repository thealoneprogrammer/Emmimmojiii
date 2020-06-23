<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <nuxt-link to="/" class="back-btn">
        <v-icon color="primary">mdi-arrow-left</v-icon>back to all emojis
      </nuxt-link>
      <br />
      <br />
      <Emojis v-for="emoji in emojis" :emoji="emoji" :key="emoji.slug" />
    </v-flex>
  </v-layout>
</template>

<script>
import Emojis from '@/components/Emojis'
import axios from 'axios'

export default {
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start()

      setTimeout(() => this.$nuxt.$loading.finish(), 2000)
    })
  },
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
        `https://emoji-api.com/categories/` +
          this.$route.params.category +
          `?access_key=${_apiKey}`,
        config
      )
      console.log(response.data)

      this.emojis = response.data
    } catch (error) {
      console.log(error)
    }
  },
  components: {
    Emojis
  }
}
</script>

<style>
.back-btn {
  text-decoration: none;
}
</style>