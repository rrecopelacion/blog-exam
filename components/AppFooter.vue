<template>
  <footer class="l-footer">
    <div class="footer-info">
      <div class="l-container">
        <div class="footer-image">
          <img
          class="img-responsive"
          src="~assets/images/footer-logo.png"
          alt="footer logo" />
        </div>
        <p class="footer-text">サンプルテキストサンプル ルテキストサンプルテキストサンプルテキストサンプル ルテキスト</p>
      </div>
    </div>
    <div class="footer-copyright" id="js-footer-copyright">
      <div class="l-container">
        <p>Copyright&copy;2007-2020 Blog Inc.</p>
      </div>
    </div>
    <button :class="`footer-back-to-top ${this.showScrollUp && 'is-active'} ${this.stickyScroll && 'is-sticky'}`"
      id="js-back-to-top"
      @click="scrollToTop()" >
      <img
        src="~assets/images/back-to-top.png"
        alt="back to top" />
      <p>TOP</p>
    </button>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  data() {
    return {
      showScrollUp: false,
      stickyScroll: false,
    }
  },
  methods: {
    handleScroll () {
      let winScroll = window.scrollY;
      let copyright = document.getElementById('js-footer-copyright');
      let sticky = document.getElementById('js-back-to-top');
      let stickyPos = (sticky.getBoundingClientRect().top + document.body.scrollTop) + sticky.offsetHeight;
      let copyrightPos = copyright.getBoundingClientRect().top + document.body.scrollTop;

      this.showScrollUp = (winScroll >= 600) ? true : false;
      this.stickyScroll = (stickyPos >= copyrightPos) ? true : false;
    },
    scrollToTop() {
      window.scrollTo({top: 0, behavior: 'smooth'});
    }
  },
  beforeMount () {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  }
}
</script>

<style scoped lang="scss" src="./Footer.scss">
