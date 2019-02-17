<template>
  <div id="app">
    <l3d :f0="f0" :f1="f1" ref="l3d" />
  </div>
</template>

<script>
import './assets/casparcg.css'
import l3d from './components/l3d.vue'

export default {
  name: 'app',
  components: {
    l3d
  },
  data () {
    return {
      f0: "",
      f1: ""
    }
  },
  mounted () {
    window.play = () => {
      this.$refs.l3d.play()
    }
    window.stop = () => {
      this.$refs.l3d.stop()
    }
    window.update = data => {
      if (typeof data === 'string') {
        data = data.replace(/^(<templateData>|<componentData>|<data>)|(<\/templateData>|<\/componentData>|<\/data>)$/ig, '')
        try {
          data = JSON.parse(decodeURI(data))
        } catch (e) {
          // data not parsed, most likely it is not json but xml. we don't handle that as of yet.
        }
      } 
      if(data && typeof data === 'object') {
        if (data.f0 !== undefined) this.f0 = data.f0
        if (data.f1 !== undefined) this.f1 = data.f1
      }
    }
    window.next = () => {}
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: bold;
  color: #2c3e50;
  position: absolute;
  width: 100%;
  height: 100%;
}
</style>
