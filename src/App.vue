<template>
  <div id="app">
    <drag-list :listData="listData" />
  </div>
</template>

<script>
import DragList from './components/DragList.vue';

export default {
  name: 'app',
  components: {
    DragList
  },

  data() {
    return {
      listData: [
        {
          label: 'Shop',
          children: [
            {
              label: 'Featured',
              children: [
                {
                  label: 'New Arrivals'
                },
                {
                  label: 'Subscriptions'
                },
                {
                  label: 'Succulents'
                },
              ]
            },
            {
              label: 'Collections',
            },
            {
              label: 'Light',
            },
          ]
        },
        {
          label: 'Plant Care',
        },
        {
          label: 'Weekly Workshops',
        },
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
