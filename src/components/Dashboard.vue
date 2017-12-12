<template>
  <div class="grid">
    <grid-layout
      :layout="layout"
      :col-num="12"
      :row-height="30"
      :is-draggable="true"
      :is-resizable="true"
      :vertical-compact="true"
      :margin="[10, 10]"
      :use-css-transforms="true"
    >
      <grid-item v-for="(item, index) in layout"
                 :x="item.x"
                 :y="item.y"
                 :w="item.w"
                 :h="item.h"
                 :i="item.i"
                 :maxH="7"
                 :minH="7"
                 :minW="3"
      >
        <dashboard-card :metrics="metrics[index]"/>
      </grid-item>
    </grid-layout>
  </div>
</template>

<script>
  import VueGridLayout from 'vue-grid-layout';
  import DashboardCard from './DashboardCard';

  const GridLayout = VueGridLayout.GridLayout;
  const GridItem = VueGridLayout.GridItem;

  export default {
    name: 'Dashboard',
    components: {
      GridLayout,
      GridItem,
      DashboardCard
    },
    data () {
      return {
        layout: [
          {"x":0,"y":0,"w":4,"h":7,"i":"0"},
          {"x":4,"y":0,"w":4,"h":7,"i":"1"},
          {"x":8,"y":0,"w":4,"h":7,"i":"2"},
          {"x":0,"y":7,"w":3,"h":7,"i":"3"},
          {"x":3,"y":7,"w":6,"h":7,"i":"4"},
          {"x":9,"y":7,"w":3,"h":7,"i":"5"},
        ],
        metrics: [
          {
            i: "0",
            name: "Ad Unit Revenue",
            type: "bars",
            data: [
              {
                name: "MRECMARF",
                values: [1100, 1200]
              },
              {
                name: "Mobile_Sticky",
                values: [743.77, 678.32]
              }
            ]
          },
          {
            i: "1",
            name: "Source Impressions",
          },
          {
            i: "2",
            name: "Location CPM",
          },
          {
            i: "3",
            name: "Device Revenue",
          },
          {
            i: "4",
            name: "My Reports",
          },
          {
            i: "5",
            name: "Device Impressions",
          },
        ],
      }
    }
  }
</script>

<style>
  .vue-grid-item {
    background-color: rgba(0,0,0,0.3);
  }
  .vue-grid-item.resizing {
    opacity: 0;
  }
  .vue-grid-item.vue-grid-placeholder {
    background: grey;
  }
</style>
