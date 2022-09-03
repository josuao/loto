<template>
   <csv-import/>
</template>
<script>

import CsvImport from './components/CsvImport.vue';
export default {
  name: "App",
  components: {
    CsvImport,
  },
  data() {
    return {
      csv: null,
    };
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
