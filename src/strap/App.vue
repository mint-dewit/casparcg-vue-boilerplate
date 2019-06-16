<template>
  <div id="app" class="fullframe">
    <strap :f0="f0" :f1="f1" ref="ticker" />
  </div>
</template>

<script>
import '../assets/casparcg.css'
import strap from './components/strap.vue'

export default {
  name: 'app',
  components: {
    strap
  },
  data () {
    return {
      f0: undefined,
      f1: undefined
    }
  },
  mounted () {
    window.play = () => {
      this.$refs.ticker.play()
    }
    window.stop = () => {
      this.$refs.ticker.stop()
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
        this.f0 = data.f0
        this.f1 = data.f1
      }
    }
    window.next = () => {}
    
    if (document.location.host === 'localhost:8080') {
      this.f0 = "Amsterdam"
      this.f1 = "Live"
      this.$refs.ticker.play()
    }
  }
}
</script>
