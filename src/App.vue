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
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

/* RESET */

* {
	font-family: arial;
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

body {
	margin: 0;
	padding: 0;
	background-color: #fff;
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
