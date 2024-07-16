<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import HomePage from './pages/HomePage.vue'

export default {
  components: {
    HomePage,
    Header,
    Footer,
  },
  data() {
    return {
      message: ''
    }
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('/api/example')
        this.message = response.data.message
      } catch (error) {
        console.error('Error fetching data:', error)
      }
    }
  }
}
</script>

<template>
  <div>
    <Header />
    <router-view></router-view>
    <Footer />
  </div>
</template>

<style scoped lang="scss">
</style>
