<template>
  <div id="app">
    <wipe ref="wipe" />
  </div>
</template>

<script>
import '../assets/casparcg.css'
import wipe from './components/wipe.vue'

export default {
  name: 'app',
  components: {
    wipe
  },
  data () {
    return {
      f0: "",
      f1: ""
    }
  },
  mounted () {
    window.play = () => {
      this.$refs.wipe.play()
    }
    window.stop = () => {
      this.$refs.wipe.stop()
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
    
    if (document.location.host === 'localhost:8080') {
      this.$refs.wipe.play()
    }
  }
}
</script>
