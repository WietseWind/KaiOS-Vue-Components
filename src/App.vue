<template>
  <div id="app">
    <Header title="KaiOS Vue Components" />

    <div>Hello World</div>

    <Softkey :softkeys.sync="softkeys" />
  </div>
</template>

<script>
import Header from './components/Header'
import Softkey from './components/Softkey'

export default {
  name: 'App',
  components: {
    Header,
    Softkey
  },
  data () {
    return {
      softkeys: {
        left: '',
        center: 'Generate',
        right: ''
      }
    }
  }
}
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
  }

  html, body, #root {
    font-family: "Open Sans", sans-serif;
    margin: 0;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    background-color: #E1E2E1 !important;
  }
</style>
