<template>
  <div class="dashboard-card">
    {{metrics.name}}
  </div>
</template>

<script>
  export default {
    name: 'DashboardCard',
    props: ['metrics'],
    data () {
      return {}
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .dashboard-card {
    background-color: red;
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
</style>
