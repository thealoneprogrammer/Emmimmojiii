<template>
  <v-tooltip v-model="show" top>
    <template v-slot:activator="{ on, attrs }">
      <p
        class="emoji"
        v-on="on"
        v-show="attrs"
        @click="copyEmoji(emoji.character)"
      >{{emoji.character}}</p>
    </template>
    <span>{{ emoji.slug }}</span>
  </v-tooltip>
</template>
<script>
export default {
  name: 'Emoji',
  props: ['emoji'],
  data() {
    return {
      show: false
    }
  },
  methods: {
    mounted() {
      this.$nextTick(() => {
        this.$nuxt.$loading.start()

        setTimeout(() => this.$nuxt.$loading.finish(), 2000)
      })
    },
    async copyEmoji(emoji) {
      try {
        await this.$copyText(emoji)
        this.$notifier.showMessage({
          content: `Copied to clipboard ${emoji}`,
          color: 'success'
        })
      } catch (error) {
        this.$notifier.showMessage({
          content: 'Error while copying!',
          color: 'error'
        })
      }
    }
  }
}
</script>

<style>
.emoji {
  padding: 1rem;
  font-size: 50px;
  transition: transform 0.2s;
  display: -webkit-inline-box;
  cursor: pointer;
}

.emoji:hover {
  transform: scale(2);
}
</style>