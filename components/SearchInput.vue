<template>
  <div>
    <!-- <input
      v-model="searchQuery"
      type="search"
      autocomplete="off"
      placeholder="Search Articles"
    /> -->
    <b-form-input 
    size="sm" 
    class="mr-sm-2 w-100" 
    v-model="searchQuery"
    type="search"
    autocomplete="off"
    placeholder="Search Articles"></b-form-input>

    <ul v-if="articles.length"
    class="bg-light list-unstyled my-3"
    >
      <li v-for="article of articles" :key="article.slug" class="mb-2 border-bottom pb-2">
        <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
          {{ article.title }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        searchQuery: '',
        articles: []
      }
    },
    watch: {
      async searchQuery(searchQuery) {
        if (!searchQuery) {
          this.articles = []
          return
        }
        this.articles = await this.$content('articles')
          .limit(6)
          .search(searchQuery)
          .fetch()
      }
    }
  }
</script>