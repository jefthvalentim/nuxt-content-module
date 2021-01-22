<template>
    <main class="container">
        <h1>{{doc.title}}</h1>
        <img :src="require(`~/assets/images/${doc.img}`)" alt="">
        <nuxt-content :document="doc"/>
    </main>
</template>

<script>
export default {
 
  async asyncData({$content, params}) {
    const doc = await $content('blog', params.slug).fetch()
    return {doc}
  }
}
</script>

<style>
    .container { max-width: 800px; margin: 50px auto; }
</style>