<!-- componentes -- Sempre comecam com <tamplate> -->

<template>
  <div id="container-box">
    <MyBox name="bru" age="19" status="active" />
    <MyBox name="daniel" age="19" status="inactive" />
    <MyBox name="anne" age="19" status="inactive" />
  </div>

</template>

<script>

import MyBox from './components/MyBox.vue';

export default {
  name: 'App',
  components: {
    MyBox
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#container-box {
  display: flex;
  flex-direction: row;
  gap: 10px;
  border: 1px solid black;
  padding: 10px;
  justify-content: center;
}
</style>
