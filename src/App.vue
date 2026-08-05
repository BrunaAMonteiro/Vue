<!-- componentes -- Sempre comecam com <tamplate> -->

<template>
  
  <div id="container-box">
    <TaskList />
  </div>

</template>

<script>


import TaskList from './components/TaskList.vue';

export default {
  name: 'App',
  components: {
    TaskList
  },

  data() {  // todas variáveis locais (só existe dentro do App)
    return {
      count: Number(localStorage.getItem('count') )|| 0
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
  },
  computed: { // variaveis calculadas baseadas na reatividade. Sempre que algo mudar, ela tambem muda. propriedades derivadas
    changeColorCount() {
      if (this.count === 0) return 'black'
      if (this.count > 0) return 'green'
      return 'red'
    },
    countState() {
      if (this.count === 0) return ''
      if (this.count > 0) return 'Positivo'
      return 'Negativo'
    }
  },
  watch: {
    count(newValue) {
      localStorage.setItem('count', newValue)
    },
    changeColorCount(newValue) {
      alert(`cor selecionada é : ${newValue}`)
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
