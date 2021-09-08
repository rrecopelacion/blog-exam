<template>
  <div>
    <Header />
    <main class="l-index">
      <Nuxt />
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from '../components/AppHeader';
import Footer from '../components/AppFooter';

export default {
  components: {
    Header,
    Footer,
  }
}
</script>
