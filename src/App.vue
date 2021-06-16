<template>
  <div id="app">
    <TheHeader />
    <router-view class="height" />
    <TheFooter />
  </div>
</template>

<script>
import TheHeader from "@/components/Layout/TheHeader.vue"
import TheFooter from "@/components/Layout/TheFooter.vue"

export default {
  name: 'App',
  components: {
    TheHeader,
    TheFooter
  },
  methods: {
    resize() {
      window.addEventListener('resize', () => {
        if(window.innerWidth > 600) {
            if(document.querySelector(".menu nav ul").classList.contains('flex'))
                document.querySelector(".menu nav ul").classList.remove('flex')
        }
      })
    },
    created() {
      this.resize()
    }
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

/* RESET */

* {
	font-family: arial;
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

html {
	scroll-behavior: smooth;
}

body {
	background-color: #efefef;
}

img {
	max-width: 100%;
	display: block;
}

.container {
	display: flex;
	justify-content: space-between;
	max-width: 990px;
	width: 100%;
	padding: 10px;
}

.height {
  min-height: calc(100vh - 133px - 164px);
}
</style>
