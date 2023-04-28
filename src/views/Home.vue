<template>
  <div>
    <v-row>
      <v-col v-for="article in articles" :key="article.id">
        <v-card class="mx-auto" width="300" height="330">
          <v-img
            class="white--text align-end"
            height="200px"
            src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
          >
            <v-card-title>{{ article.title }}</v-card-title>
          </v-img>

          <v-card-text class="text--primary">
            {{ article.description }}
          </v-card-text>

          <v-card-actions>
            <router-link
              :to="{ name: 'article-detail', params: { id: article.id } }"
            >
              <v-btn color="orange" text>More</v-btn>
            </router-link>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Home',

  data: () => ({
    articles: [],
  }),

  async mounted() {
    // 記事を取得する
    const response = await axios.get(
      'https://madokaumezawa.microcms.io/api/v1/articles',
      {
        headers: {
          'X-MICROCMS-API-KEY': '226a40393fa841ddae134fb040cf8d0959d9',
        },
      }
    );
    this.articles = response.data.contents;
  },
};
</script>

<style scoped>
.summary {
  white-space: pre-wrap;
}
</style>
