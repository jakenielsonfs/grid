<template>
  <div class="dashboard-card">
    <span class="card-name">{{metrics.name}} - x:{{layout.x}} y:{{layout.y}} w:{{layout.w}} i:{{layout.i}}</span>
    <div class="card-metric" v-for="metric in metrics.data" :key="metric.name">
      <div class="card-metric-left">
        <span class="card-metric-name">{{metric.name}}</span>
        <div class="card-metric-bar-wrapper">
          <span class="card-metric-bar" v-for="value in metric.values" :key="value" :style="{width: getLength(value)}"></span>
        </div>
      </div>
      <div class="card-metric-right">
        <div class="card-metric-value-wrapper">
          <span class="card-metric-value" v-for="value in metric.values" :key="value">{{value}}</span>
        </div>
        <i class="card-metric-icon fa" :class="{
            'fa-long-arrow-up': metric.values[0] > metric.values[1],
            'fa-long-arrow-down': metric.values[1] > metric.values[0],
            'fa-arrows-v': metric.values[0] === metric.values[1]
          }"></i>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'DashboardCard',
    props: ['metrics', 'layout'],
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
    height: calc(100% - 60px);
    width: calc(100% - 30px);
    border-radius: 2px;
    background-color: #FFFFFF;
    box-shadow: 0 1px 2px 0 rgba(0,0,0,0.3);
    padding: 30px 15px;
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
    width: calc(100% - 80px);
    display: flex;
    flex-direction: column;
    margin-right: 20px;
  }
  .card-metric-right {
    width: 80px;
    display: flex;
    flex-direction: row;
  }
  .card-metric-value-wrapper {
    display: flex;
    width: 70px;
    flex-direction: column;
    text-align: right;
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
  .card-metric-bar-wrapper {
    width: 100%;
    height: 100%;
  }
  .card-metric-bar {
    height: 3px;
    margin-top: 3px;
    background: #DBE0E2;
    display: block;
  }
  .card-metric-bar:first-child {
    background: #2B2C31;
  }
  .card-metric-value {
    font-size: 12px;
    line-height: 15px;
    color: #A3ABB6;
    font-weight: 500;
  }
  .card-metric-value:first-child {
    color: #5A677A;
    font-size: 16px;
  }
  .card-metric-icon {
    margin-top: 5px;
    width: 5px;
    margin-left: 15px;
    font-size: 12px;
  }
  .fa-long-arrow-up {
    color: #3ECF8E;
  }
  .fa-long-arrow-down {
    color: #DBE0E2;
  }
</style>
