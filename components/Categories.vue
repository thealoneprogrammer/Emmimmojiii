<template>
  <v-expansion-panels>
    <v-expansion-panel>
      <v-expansion-panel-header>
        Search by category
        <template v-slot:actions>
          <v-icon color="primary">$expand</v-icon>
        </template>
      </v-expansion-panel-header>
      <v-expansion-panel-content>
        <v-list rounded>
          <v-list-item-group v-model="item" color="primary">
            <v-list-item v-for="(item, i) in items" :key="i">
              <v-list-item-icon>
                <v-avatar class="yellow darken-4">{{ i + 1 }}</v-avatar>
              </v-list-item-icon>
              <v-list-item-content>
                <nuxt-link :to="'categories/' + item.slug " class="link">
                  <v-list-item-title v-text="item.slug"></v-list-item-title>
                </nuxt-link>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-expansion-panel-content>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Categories',
  data: () => ({
    item: 1,
    items: [],
  }),
  async created() {
    const _apiKey = process.env.emoji_api_key
    const config = {
      headers: {
        accept: 'application/json'
      }
    }
    try {
      const response = await axios.get(
        `https://emoji-api.com/categories?access_key=${_apiKey}`,
        config
      )

      this.items = response.data

      console.log(response.data)
    } catch (error) {
      console.log(error)
    }
  }
}
</script>

<style>
  .link{
    text-decoration: none;
  }
</style>