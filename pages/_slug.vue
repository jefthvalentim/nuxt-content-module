<template>
  <div>
    <input type="text" name="" v-model="search" @input="$fetch">
    <div v-for="file in files">
      <p>{{file.title}}</p>
      <p>{{file.description}}</p>
    </div>
  </div>
</template>

<script>
export default {
 
  data() {
    return {
      search: '',
      files: []
    }
  },
  async fetch() {
    this.files = await this.$content('movies').search(this.search).fetch()
  }
}
</script>
