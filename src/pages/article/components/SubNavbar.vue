<template>
  <div class="subnavbar-main">
    <div class="subnavbar-items">
      <router-link to="/">
        <div v-if="homeCarouselItem.length" class="subnavbar-title">
          {{ homeCarouselItem.title }}
        </div>
      </router-link>
      <button v-for="item in blogTypeItems" :key="item.id" class="subnavbar-tab">
        {{ item.type_name }}
      </button>
    </div>
  </div>
</template>

<script>
import { getHomeCarousel, getBlogType } from '@/api/blog'

export default {
  name: 'SubNavbar',
  data () {
    return {
      appTitle: 'SubNavbar',
      sidebar: false,
      homeCarouselItem: [],
      blogTypeItems: []
    }
  },
  mounted () {
    this.getBlogType()
    this.getHomeCarousel()
  },
  methods: {
    getHomeCarousel () {
      return new Promise((resolve, reject) => {
        getHomeCarousel(this.$store.getters['domain/domain'])
          .then((response) => {
            // console.log(JSON.stringify(response))
            if (response.length) {
              this.homeCarouselItem = response[0]
            }
            resolve()
          })
          .catch((error) => {
            reject(error)
          })
      })
    },
    getBlogType () {
      return new Promise((resolve, reject) => {
        getBlogType(this.$store.getters['domain/domain'])
          .then((response) => {
            // console.log(JSON.stringify(response))
            this.blogTypeItems = response
            resolve()
          })
          .catch((error) => {
            reject(error)
          })
      })
    }
  }
}
</script>
<style>
@media (max-width: 979px) {
  .subnavbar-main {
    display: flex;
    align-items: center;
    background-color: #fff;
    height: 15vh;
    border-top: 1px solid rgba(0, 0, 0, 0.1);
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    margin-bottom: 3vh;
  }

  .subnavbar-items {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    width: 100%;
    padding-left: 10vw;
    padding-right: 10vw;
  }

  .subnavbar-tab {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: flex-start;
    color: rgba(0, 0, 0, 0.54);
    margin-left: 2vw;
    margin-right: 2vw;
  }
}

@media (min-width: 980px) {
  .subnavbar-main {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    background-color: #fff;
    height: 8vh;
    border-top: 1px solid rgba(0, 0, 0, 0.1);
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    margin-bottom: 3vh;
  }

  .subnavbar-items {
    display: flex;
    align-items: center;
    width: 100%;
    padding-left: 15vw;
    padding-right: 15vw;
  }

  .subnavbar-tab {
    font-size: 1rem;
    color: rgba(0, 0, 0, 0.54);
    margin-left: 1vw;
    margin-right: 1vw;
  }
}

.subnavbar-items > a {
  text-decoration: none;
}

.subnavbar-title {
  font-size: 1.25rem;
  font-weight: 300;
  color: #000;
}

</style>
