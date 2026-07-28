<!-- componentes -- Sempre comecam com <tamplate> -->

<template>
  <div id="container-box">
    <!--<MyBox name="bru" age="19" status="active" />-->
    <h2>{{ count }}</h2>
    <CounterButtons @change-count="handleCountChange"/>

  </div>

</template>

<script>

// import MyBox from './components/MyBox.vue';
// import MyButton from './components/MyButton.vue';
import CounterButtons from './components/CounterButtons.vue';

export default {
  name: 'App',
  components: {
    CounterButtons
  },

  data() {  // todas variáveis locais (só existe dentro do App)
    return {
      count: 0
    }
  },
  methods: {
    handleCountChange(action, value = 1) {
      switch (action) {

        case 'increment':
          this.count += value
          break
        case 'decrement':
          this.count -= value
          break
        case 'reset':
          this.count = 0
          break
      }
    }
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
