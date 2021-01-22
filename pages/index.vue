<template>
<section class="container">
  <div class="">
    <h1 class="title">Posts</h1>
    <p>Listagem de post do meu blog.</p>
  </div>
  <div class="post-container">
    <div class="post-item" v-for="article in articles" :key="article.id">
    <nuxt-link :to="{ name: 'blog-slug', params: { slug: article.slug }}">
      <div class="border border-gray-200 p-1 rounded-lg">
        <div class="w-100 inline-flex items-center justify-center rounded-full bg-indigo-100 text-indigo-500 mb-4">
          <img :src="require(`~/assets/images/${article.img}`)" alt="">
        </div>
        <h2 class="text-lg text-gray-900 font-medium title-font mb-2">{{article.title}}</h2>
        <p class="leading-relaxed text-base">{{article.description}}</p>
      </div>
    </nuxt-link>
    </div>
  </div>
</section>
</template>

<script>
export default {
  data(){
    return {
      articles: []
    }
  },

  async asyncData({$content}) {
    const articles = await $content('blog').only(['title', 'description', 'img', 'slug']).sortBy('CreatedAt', 'DESC').fetch()
    return {articles}
  }
}
</script>
<style>
  .container{ max-width: 1360px; margin: auto; }
  .post-container { display: flex; flex-wrap: wrap; }
  .post-item{ width: 300px; margin: 0 15px; }
  .post-item:first-child{ margin-left: 0; }
  img { max-width: 100%; }
</style>