<template>
  <div class="subnavbar-main">
    <div class="subnavbar-tab">
      <button :class="[subnavbarActive == '' ? activeClass : errorClass]" @click="getBlog('')">
        全部
      </button>
      <button v-for="item in items" :key="item.id" :class="[subnavbarActive == item.type_name ? activeClass : errorClass]" @click="getBlog(item.type_name)">
        {{ item.type_name }}
      </button>
    </div>
  </div>
</template>

<script>
import { getBlogType } from '@/api/blog'

export default {
  name: 'SubNavbar',
  data () {
    return {
      activeClass: 'subnavbar-tab-item-active',
      errorClass: 'subnavbar-tab-item',
      appTitle: 'SubNavbar',
      sidebar: false,
      items: []
    }
  },
  computed: {
    subnavbarActive () {
      return this.$store.getters['blog/getSubnavbarActive']
    }

  },
  mounted () {
    this.getBlogType()
  },
  methods: {
    getBlogType () {
      return new Promise((resolve, reject) => {
        getBlogType(this.$store.getters['domain/domain'])
          .then((response) => {
            // console.log(JSON.stringify(response))
            this.items = response
            resolve()
          })
          .catch((error) => {
            reject(error)
          })
      })
    },
    getBlog (type) {
      const obj = {
        typeName: type,
        backendUrl: this.$store.getters['domain/domain']
      }
      this.$store.dispatch('blog/switchLatest', obj)
    }
  }
}
</script>
<style>
@media (max-width: 979px) {
  .subnavbar-main {
    display: flex;
    flex-wrap: wrap;
    height: 15vh;
    margin-top: 5vh;
    background-color: #fff;
    width: 100%;
    font-size: 1.5rem;
    color: rgba(0, 0, 0, 0.54);
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    margin-bottom: 3vh;
  }

  .subnavbar-tab {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: flex-start;
  }

  .subnavbar-tab > button {
    margin-left: 5vw;
    margin-right: 5vw;
  }
}

@media (min-width: 980px) {
  .subnavbar-main {
    display: flex;
    height: 8vh;
    background-color: #fff;
    width: 100%;
    font-size: 1rem;
    color: rgba(0, 0, 0, 0.54);
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    margin-bottom: 3vh;
  }

  .subnavbar-tab {
    display: flex;
    align-items: center;
  }

  .subnavbar-tab > button {
    margin-left: 1vw;
    margin-right: 1vw;
  }
}

.subnavbar-tab-item-active {
  font-weight: 700;
  color: #000;
}

.subnavbar-tab-item {
  font-weight: 500;
}

</style>
