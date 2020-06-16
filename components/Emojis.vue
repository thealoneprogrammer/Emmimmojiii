<template>
  <v-tooltip v-model="show" top>
    <template v-slot:activator="{ on, attrs }">
      <span class="emoji" v-bind="attrs" v-on="on">{{emoji.character}}</span>
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
  }
}
</script>

<style>
.emoji {
  padding: 1rem;
  font-size: 50px;
}
</style>