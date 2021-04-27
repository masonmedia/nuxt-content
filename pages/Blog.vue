<template>
  <section-wrap
  fluid
  contClass="mt-5"
  rowClass="p-5">
    <b-col xl="12" class="mb-5">
        <h1 class="font-weight-bold">Posts</h1>
    </b-col>
    
    <b-col lg="6" 
    class="" 
    style="min-height: 25vh;"
    v-for="article of articles" :key="article.slug">
        <b-card 
        no-body 
        class="shadow-lg overflow-hidden mb-3" 
        >
        <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
            <b-row no-gutters>
            <b-col md="6">
                <b-card-img 
                :src="article.img" 
                alt="Image" 
                class="rounded-0 card-img h-100 w-100"
                style="objecxt-fit: cover;"></b-card-img>
            </b-col>
                <b-col md="6">
                    <b-card-body :title="article.title">
                    <b-card-text>
                        <p class="">{{ article.description }}</p>
                        <p class="text-muted">by {{ article.author.name }}</p>
                    </b-card-text>
                    </b-card-body>
                </b-col>
            </b-row>
        </NuxtLink>
    </b-card>
    </b-col>

    <!-- <b-col>
<ul class="flex flex-wrap mb-4 text-center">
      <li
        v-for="tag of tags"
        :key="tag.slug"
        class="xs:w-full md:w-1/3 lg:flex-1 px-2 text-center"
      >
        <NuxtLink :to="`/blog/tag/${tag.slug}`" class="">
          <p
            class="font-bold text-gray-600 uppercase tracking-wider font-medium text-ss"
          >
            {{ tag.name }}
          </p>
        </NuxtLink>
      </li>
    </ul>
        </b-col> -->
  </section-wrap>
</template>

<script>
  export default {
      name: 'Blog',
        async asyncData({ $content, params }) {
        const articles = await $content('articles')
            .only(['title', 'description', 'img', 'slug', 'author'])
            .sortBy('createdAt', 'asc')
            .fetch()
            // const tags = await $content('tags', params.slug)
            // .only(['name', 'description', 'img', 'slug'])
            // .sortBy('createdAt', 'asc')
            // .fetch()
        return {
            articles,
            // tags
        }
    },
    mounted() {
        this.staggering()
    },
    methods: {
        staggering() {
        const gsap = this.$gsap
        gsap.from('.card', {
            x: -100,
            stagger: 0.1,
            opacity: 0,
            duration: 1,
            ease: 'back.inOut(1.7)',
        })
        }
    }
  }
</script>