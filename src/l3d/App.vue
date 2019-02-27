<template>
  <div id="app" class="fullframe">
    <l3d-two-name v-if="f2 || f3"  :f0="f0" :f1="f1" :f2="f2" :f3="f3" ref="l3d" />
    <l3d v-else :f0="f0" :f1="f1" ref="l3d" />
  </div>
</template>

<script>
import '../assets/casparcg.css'
import l3d from './components/l3d.vue'
import l3dTwoName from './components/l3dTwoName.vue'

export default {
  name: 'app',
  components: {
    l3d, l3dTwoName
  },
  data () {
    return {
      f0: undefined,
      f1: undefined,
      f2: undefined,
      f3: undefined
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
        this.f0 = data.f0
        this.f1 = data.f1
        this.f2 = data.f2
        this.f3 = data.f3
      }
    }
    window.next = () => {}
    
    if (document.location.host === 'localhost:8080') {
      this.f0 = "Balte"
      this.f1 = "Developer"
      this.$refs.l3d.play()
    }
  }
}
</script>
