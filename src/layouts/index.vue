<template>
  <div class="app-wrapper">
    <div class="header">
      <app-navbar />
      <app-header />
    </div>
    <div class="main">
      <app-main />
    </div>
    <div class="footer">
      <app-footer />
    </div>
  </div>
</template>

<script>
import AppMain from './components/AppMain.vue'
import AppHeader from './components/AppHeader.vue'
import AppNavbar from './components/AppNavbar.vue'
import AppFooter from './components/AppFooter.vue'

export default {
  name: 'Layout',
  components: {
    AppMain,
    AppHeader,
    AppNavbar,
    AppFooter
  },
  middleware: [
    'domain'
  ],
  head () {
    return {
      titleTemplate: `%s | ${this.$store.getters['domain/subtitle']}`,
      title: this.$store.getters['domain/title'],
      meta: [
        { hid: 'title', name: 'title', content: this.$store.getters['domain/title'] },
        { hid: 'description', name: 'description', content: this.$store.getters['domain/subtitle'] },
        { hid: 'site_name', name: 'site_name', content: this.$store.getters['domain/subtitle'] },
        { hid: 'locale', name: 'locale', content: 'zh_TW' },
        { hid: 'og:title', property: 'og:title', content: this.$store.getters['domain/title'] },
        { hid: 'og:description', property: 'og:description', content: this.$store.getters['domain/subtitle'] },
        { hid: 'og:image', property: 'og:image', content: this.$store.getters['domain/banner'] },
        { hid: 'apple-mobile-web-app-title', property: 'apple-mobile-web-app-title', content: this.$store.getters['domain/subtitle'] },
        { hid: 'og:site_name', property: 'og:site_name', content: this.$store.getters['domain/title'] },
        { hid: 'og:locale', property: 'og:locale', content: 'zh_TW' },
        { hid: 'og:url', property: 'og:url', content: 'https://' + this.$store.getters['domain/host'] }
      ],
      htmlAttrs: {
        lang: 'zh-TW'
      },
      link: [
        {
          hid: 'canonical',
          rel: 'canonical',
          href: 'https://' + this.$store.getters['domain/host']
        }
      ],
      script: [
        {
          src: 'https://www.googletagmanager.com/gtag/js?id=G-' + process.env.GOOGLE_TAG,
          innerHTML: 'window.dataLayer = window.dataLayer || [];',
          'data-ad-client': 'ca-pub-G-' + process.env.GOOGLE_TAG,
          async: true
        }
      ]
    }
  },
  mounted () {
    function gtag () { window.dataLayer.push(arguments) }
    gtag('js', new Date())

    gtag('config', 'G-' + process.env.GOOGLE_TAG)
  }

}
</script>

<style lang="scss" scoped>
@media (max-width: 750px) {
  .app-wrapper {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: 10vh auto  15vh;
  }

  .header {
    grid-column: span 12;
  }

  .main {
    grid-column: span 12;
  }

  .footer {
    grid-column: span 12;
  }
}

@media (min-width: 750px) {
  .app-wrapper {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: 6.6vh auto  15vh;
  }

  .header {
    grid-column: span 12;
  }

  .main {
    grid-column: span 12;
  }

  .footer {
    grid-column: span 12;
  }
}

</style>
