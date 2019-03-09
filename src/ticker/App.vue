<template>
  <div id="app" class="fullframe">
    <ticker :f0="f0" ref="ticker" />
  </div>
</template>

<script>
import '../assets/casparcg.css'
import ticker from './components/ticker.vue'

export default {
  name: 'app',
  components: {
    ticker
  },
  data () {
    return {
      f0: undefined
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
      }
    }
    window.next = () => {}
    
    if (document.location.host === 'localhost:8080') {
      this.f0 = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."
      this.$refs.ticker.play()
    }
  }
}
</script>
