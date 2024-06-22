<template>
  <div id="app">
    
    <MobileView v-if="isMobile" />
    <DesktopView v-else />
   
  </div>
</template>

<style lang="scss" >
@import url('https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,300..900;1,300..900&display=swap');
* {
  font-family: "Rubik", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>>

<script>
import MobileView from './components/PhoneView.vue';
import DesktopView from './components/Home.vue';
import Footer from './components/Footer.vue'

export default {
  components: { MobileView, DesktopView },
  data() {
    return {
      windowWidth: window.innerWidth,
    };
  },
  computed: {
    isMobile() {
      return this.windowWidth <= 767; // Adjust the breakpoint as needed
    }
  },
  mounted() {
    window.addEventListener('resize', this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    handleResize() {
      this.windowWidth = window.innerWidth;
    }
  }
};
</script>
