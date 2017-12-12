<template>
  <div class="dashboard-card">
    <span class="card-name">{{metrics.name}}</span>
    <div class="card-metric" v-for="metric in metrics.data">
      <div class="card-metric-left">
        <span class="card-metric-name">{{metric.name}}</span>
        <span class="card-metric-bar" v-for="value in metric.values" :class="{'card-metric-bar-active': isLargestValue(metric, value)}" :style="{width: getLength(value)}"></span>
      </div>
      <div class="card-metric-right">
        <span class="card-metric-value" v-for="value in metric.values" :class="{'card-metric-value-active': isLargestValue(metric, value)}">{{value}}</span>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'DashboardCard',
    props: ['metrics'],
    data () {
      return {}
    },
    methods: {
      getLargestValue(metric) {
        let largestValue = 0;
        for (let i=0; i<metric.values.length; i++) {
          if (metric.values[i] > largestValue) {
            largestValue = metric.values[i];
          }
        }
        return largestValue;
      },
      getLength(value) {
        let largestValue = 0;
        for (let i=0; i<this.metrics.data.length; i++) {
          if (this.getLargestValue(this.metrics.data[i]) > largestValue) {
            largestValue = this.getLargestValue(this.metrics.data[i]);
          }
        }
        return `${(value / largestValue) * 100}%`;
      },
      isLargestValue(metric, value) {
        const largestValue = this.getLargestValue(metric);
        return value === largestValue;
      }
    }
  }
</script>

<style scoped>
  .dashboard-card {
    display: flex;
    flex-direction: column;
    height: calc(100% - 40px);
    width: calc(100% - 20px);
    border-radius: 2px;
    background-color: #FFFFFF;
    box-shadow: 0 1px 2px 0 rgba(0,0,0,0.3);
    padding: 20px 10px;
    user-select: none;
  }
  .card-name {
    text-align: left;
    font-weight: 600;
    font-size: 13px;
    letter-spacing: 1px;
    line-height: 16px;
    text-transform: uppercase;
  }
  .card-metric {
    text-align: left;
    display: flex;
    flex-direction: row;
    margin-top: 20px;
  }
  .card-metric-left {
    width: calc(100% - 50px);
    display: flex;
    flex-direction: column;
    margin-right: 20px;
  }
  .card-metric-right {
    width: 50px;
    display: flex;
    flex-direction: column;
  }
  .card-metric-name {
    font-size: 12px;
    line-height: 15px;
    margin-bottom: 5px;
  }
  .card-metric-value {
    font-size: 10px;
    color: #A3ABB6;
    margin-top: 5px;
  }
  .card-metric-bar {
    height: 3px;
    margin-top: 3px;
    background: #DBE0E2;
  }
  .card-metric-bar-active {
    background: #2B2C31;
  }
  .card-metric-value {
    font-size: 12px;
    line-height: 15px;
    color: #DBE0E2;
  }
  .card-metric-value-active {
    color: #2B2C31;
  }
</style>
