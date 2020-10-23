<template>
  <div class="stats-component">
    <h3>Аналитика по визитам</h3>
    <br/>
    <div class="container">
      <chart :chartdata="chartData" :options="chartOptions" />
    </div>
  </div>
</template>

<script>
import chart from "../components/chart.vue";

export default {
  components: {
    chart
  },
  mounted: function() {
    if (!localStorage.getItem("key")) {
      this.$router.push("/auth");
    }
  }
};
</script>
<style lang="scss">

</style>>