<template>
<div>
  <TheBanner />
  <TheGeneral />
</div>
</template>

<script>
import TheBanner from "@/components/Home/TheBanner.vue"
import TheGeneral from "@/components/Home/TheGeneral.vue"

export default {
  name: 'Home',
  components: {
    TheBanner,
    TheGeneral
  }
}
</script>

<style scoped>

</style>
