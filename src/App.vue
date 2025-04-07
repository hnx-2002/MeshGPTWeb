<template>
  <div id="app">
    <div class="page-container">
      <HeaderTitle />
      <MyDivider />
      <MeshViewer />
      <MyDivider />
      </div>
  </div>
</template>


<script>
import HeaderTitle from './components/HeaderTitle.vue'
import MeshViewer from './components/MeshViewer.vue'
import MyDivider from './components/MyDivider.vue'


export default {
  name: 'App',
  components: {
    HeaderTitle,
    MyDivider,
    MeshViewer
  }
}
</script>

<style>

html, body {
  margin: 0;
  padding: 0;
  overflow: auto;
  background-color: #ffffff;
}

.page-container {
  width: 1100px;
  margin: 0 auto; /* 水平居中 */
  background-color: white;
}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* margin-top: 60px; */
}

</style>