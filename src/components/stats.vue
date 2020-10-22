<template>
  <div class="stats-component">
    <h3>Аналитика по визитам</h3>

  </div>
</template>

<script>
export default {
  mounted: function () {
    if (!localStorage.getItem('key')) {
      this.$router.push('/auth')
    }
  },

}
</script>

<style>

</style>