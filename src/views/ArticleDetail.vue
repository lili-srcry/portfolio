<template>
  <v-card flat>
    <v-card-title>{{ article.title }}</v-card-title>

    <v-card-text>
      <div v-html="article.contents"></div>
    </v-card-text>
  </v-card>
</template>

<script>
import axios from 'axios';

export default {
  name: 'ArticleDetail',

  data: () => ({
    article: {},
  }),

  async mounted() {
    // idを指定して特定の記事を取得する
    const response = await axios.get(
      'https://madokaumezawa.microcms.io/api/v1/articles/' +
        this.$route.params.id,
      {
        headers: {
          'X-MICROCMS-API-KEY': '226a40393fa841ddae134fb040cf8d0959d9',
        },
      }
    );
    this.article = response.data;
  },
};
</script>
