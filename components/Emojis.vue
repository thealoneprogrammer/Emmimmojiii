<template>
  <v-tooltip v-model="show" top>
    <template v-slot:activator="{ on, attrs }">
      <p class="emoji" v-on="on" v-show="attrs">{{emoji.character}}</p>
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
  transition: transform 0.2s;
  display: -webkit-inline-box;
  cursor: pointer;
}

.emoji:hover {
  transform: scale(2);
}
</style>