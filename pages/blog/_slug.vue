<template>
    <article>
        <section-wrap
        fluid
        rowClass="pt-5">
        <!-- img + title col -->
            <b-col lg="6" class="p-0 fixed" style="min-height: 50vh; z-index: -1;">
                <b-img 
                class="h-100 w-100"
                style="min-height: 100vh; object-fit: cover;"
                :src="article.img" :alt="article.alt"></b-img>
                <div 
                class="text-light mt-5 p-5" 
                style="position: absolute; z-index: 100; top: 0">
                    <p class="mb-2">Article last updated: {{ formatDate(article.updatedAt) }}</p>
                    <h1 class="display-4 font-weight-bold">{{ article.title }}</h1>
                    <p class="h5 mb-4">{{ article.description }}</p>
                    <p class="border border-light p-2 rounded d-inline">{{ article.tags }}</p>
                </div>
            </b-col>
            <!-- article content -->
            <b-col lg="6" 
            offset-lg="6" 
            class="h-100 w-100 p-5">
            <!-- table of contents -->
                <!-- <nav>
                    <ul>
                        <li v-for="link of article.toc" :key="link.id">
                        <NuxtLink 
                        :to="`#${link.id}`" 
                        :class="{ 'py-2': link.depth === 2, 'ml-2 pb-2': link.depth === 3 }">
                            {{ link.text }}
                        </NuxtLink>
                        </li>
                    </ul>
                </nav> -->
                <h1 class="font-weight-bold trigger">{{ article.title }}</h1>
                <p class="mb-0">{{ article.description }}</p>
                <p>Article last updated: {{ formatDate(article.updatedAt) }}</p>
                <!-- <pre>{{ article.toc }}</pre> -->
                <hr class="text-secondary my-4" />
                <nuxt-content class="box" :document="article" />

                <author :author="article.author" />

                <prev-next :prev="prev" :next="next"  />
            </b-col>
        </section-wrap>
    </article>
</template>


<script>
import PrevNext from '../../components/PrevNext.vue'
import SectionWrap from '../../components/global/SectionWrap.vue'

  export default {
  components: { PrevNext, SectionWrap },
    async asyncData({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()
//   const tags = await $content('tags', params.slug)
//       .only(['name', 'description', 'img', 'slug'])
//       .fetch()
    const [prev, next] = await $content('articles')
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(params.slug)
      .fetch()
    return {
      article,
    //   tags,
      prev,
      next
    }
    },
    methods: {
        formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' }
        return new Date(date).toLocaleDateString('en', options)
        },
        animateOnScroll() {
        this.$gsap.from('.box', {
            y: 200,
            opacity: 0,
            duration: 0.5,
            ease: 'Power1.easeInOut',
            // https://greensock.com/docs/v3/Plugins/ScrollTrigger
            scrollTrigger: {
            trigger: '.trigger',
            start: "top top",
            //   pin: true,
            //   end: 'bottom',
            // parallax
            // scrub: 1,
            scrub: false
        }
      })
    }
    },
    mounted() {
    this.animateOnScroll()
  },
  }
</script>

<style>

.fixed {
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    z-index: 1030;
}
  .nuxt-content h2 {
    font-weight: bold;
    font-size: 28px;
  }
  .nuxt-content h3 {
    font-weight: bold;
    font-size: 22px;
  }
  .nuxt-content p {
    margin-bottom: 20px;
  }

 @media(max-width: 992px) {
     .fixed {
         position: static;
     }
 }
 
</style>
