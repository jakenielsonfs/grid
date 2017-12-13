<template>
  <div class="grid">
    <grid-layout
      :layout="layout"
      :col-num="12"
      :row-height="240"
      :is-draggable="true"
      :is-resizable="true"
      :vertical-compact="false"
      :margin="[10, 10]"
      :use-css-transforms="true"
    >
      <grid-item v-for="(item, index) in layout"
                 :x="item.x"
                 :y="item.y"
                 :w="item.w"
                 :h="item.h"
                 :i="item.i"
                 :maxH="1"
                 :minH="1"
                 :minW="3"
                 :key="item.i"
                 @resized="resize"
      >
        <dashboard-card :layout="item" :metrics="metrics[index]"/>
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
          {"x":0,"y":0,"w":4,"h":1,"i":"0"},
          {"x":4,"y":0,"w":4,"h":1,"i":"1"},
          {"x":8,"y":0,"w":4,"h":1,"i":"2"},
          {"x":0,"y":1,"w":3,"h":1,"i":"3"},
          {"x":3,"y":1,"w":6,"h":1,"i":"4"},
          {"x":9,"y":1,"w":3,"h":1,"i":"5"},
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
              },
              {
                name: 'InA-LB1',
                values: [192.32, 378.32]
              },
              {
                name: 'LB1',
                values: [92.21, 87.44]
              }
            ]
          },
          {
            i: "1",
            name: "Source Impressions",
            data: [
              {
                name: "Rubbicon",
                values: [21234, 24543]
              },
              {
                name: "Google Ad Exchange",
                values: [15029, 13435]
              },
              {
                name: "Appnexus",
                values: [500, 432]
              },
              {
                name: "Sovrn",
                values: [98, 74]
              }
            ]
          },
          {
            i: "2",
            name: "Location CPM",
            data: [
              {
                name: "United States",
                values: [1100, 1200]
              },
              {
                name: "United Kingdom",
                values: [743.77, 678.32]
              },
              {
                name: "Canada",
                values: [192.32, 378.32]
              },
              {
                name: "China",
                values: [92.21, 87.44]
              }
            ]
          },
          {
            i: "3",
            name: "Device Revenue",
            data: [
              {
                name: "Mobile",
                values: [1100, 1200]
              },
              {
                name: "Desktop",
                values: [743.77, 678.32]
              },
              {
                name: "Tablet",
                values: [192.32, 378.32]
              },
            ]
          },
          {
            i: "4",
            name: "My Reports",
            data: []
          },
          {
            i: "5",
            name: "Device Impressions",
            data: [
              {
                name: "Mobile",
                values: [1000, 1200]
              },
              {
                name: "Desktop",
                values: [532, 624]
              },
              {
                name: "Tablet",
                values: [399, 245]
              },
            ]
          },
        ],
      }
    },
    methods: {
      resize() {
        for (let i=1; i < this.layout.length; i++) {
          if (this.layout[i].y === this.layout[i-1].y && this.layout[i].x > this.layout[i-1].x + this.layout[i-1].w) {
            const prevX = this.layout[i].x;
            this.layout[i].x = this.layout[i-1].x + this.layout[i-1].w;
            this.layout[i].w += prevX - this.layout[i].x;
          }
        }
      },
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
