<template>
  <div id="app">
    <Header title="KaiOS Vue Components" />

    <div>
      Hello World
      <!-- {{ snapshot }} -->

      <keep-alive>
        <Sample1 v-if="show === 1" style="display: block; width: 400px; height: 400px; border: 1px solid red;" :state.sync="softkeys" :snapshot="softkeySnapshot" />
      </keep-alive>
      <keep-alive>
        <Sample2 v-if="show === 2" style="display: block; width: 400px; height: 400px; border: 1px solid blue;" :state.sync="softkeys" :snapshot="softkeySnapshot" />
      </keep-alive>

      <button @click="show=0; resetSoftkeys()">Show none, Reset</button>
      <button @click="show=1">Show 1</button>
      <button @click="show=2">Show 2</button>
    </div>

    <Softkey :softkeys.sync="softkeys" />
  </div>
</template>

<script>
import Header from './components/Header'
import Softkey from './components/Softkey'

import Sample1 from './components/Sample1'
import Sample2 from './components/Sample2'

export default {
  name: 'App',
  components: {
    Header,
    Softkey,

    Sample1,
    Sample2
  },
  methods: {
    // restoreSoftkeySnapshot () {
    //   if (this.snapshot.length > 0) {
    //     Object.keys(this.snapshot[0]).forEach(k => {
    //       this.softkeys[k] = this.snapshot[0][k]
    //     })
    //     this.snapshot.shift()
    //   }
    // },
    resetSoftkeys () {
      this.softkeys.left = ''
      this.softkeys.center = 'Generate'
      this.softkeys.right = ''
    },
    softkeySnapshot (component) {
      this.snapshot.push({ component, ...(this.softkeys) })
    }
  },
  mounted () {
    this.resetSoftkeys()
  },
  data () {
    return {
      show: 0,
      snapshot: [],
      softkeys: {
        left: '',
        center: '',
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
