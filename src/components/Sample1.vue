<template>
  <div>
    Sample 1
    {{ currentSoftkeys }}
    <input type="text" v-model="text" style="width: 100%">
    <button @click="otherState()">1 Other state</button>
    <button @click="setInitialState()">1 Reset state</button>
  </div>
</template>

<script>
export default {
  name: 'Sample1',
  data () {
    return {
      text: '...',
      initialized: false,
      currentSoftkeys: {
        left: '',
        center: '',
        right: ''
      }
    }
  },
  props: {
    snapshot: Function,
    state: {
      left: String,
      center: String,
      right: String
    }
  },
  methods: {
    persistCurrentSoftkeys () {
      Object.keys(this.state).forEach(k => {
        this.currentSoftkeys[k] = String(this.state[k])
      })
    },
    restoreState () {
      Object.keys(this.currentSoftkeys).forEach(k => {
        this.state[k] = String(this.currentSoftkeys[k])
      })
    },
    otherState () {
      this.state.left = 'os L'
      this.state.right = 'os R'
      this.persistCurrentSoftkeys()
    },
    setInitialState () {
      this.state.left = '1l'
      this.state.center = 'OK 1'
      this.state.right = '1r'
      this.persistCurrentSoftkeys()
    }
  },
  activated () {
    console.log('activated 1')
    // First snapshot prev. state at parent
    if (this.initialized) {
      this.restoreState()
    } else {
      this.setInitialState()
      this.initialized = true
    }
    this.snapshot('Sample1')
  }
}
</script>

<style lang="scss" scoped>
</style>
