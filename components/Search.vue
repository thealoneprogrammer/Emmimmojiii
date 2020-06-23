<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-text-field
          clearable
          solo
          label="Search for an Emoji 😂"
          prepend-inner-icon="mdi-magnify"
          @keyup="search"
          v-model="query"
        ></v-text-field>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Search',
  data() {
    return {
      query: '',
    }
  },
  methods: {
    search: async function() {
     this.$emit("search-emoji", this.query)
    }
  }
}
</script>

<style>
.v-text-field.v-text-field--solo .v-input__control {
  min-height: 80px;
  width: 500px;
  border-radius: 20px;
}
</style>