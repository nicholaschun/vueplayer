<template>
  <div id="app">
    <VideoPlayer :vidSrc="vidSrc" width="100%" type="video/mp4" />
  </div>
</template>

<script>
import VideoPlayer from './components/VideoPlayer.vue'

export default {
  name: 'app',
  data () {
    return {
      vidSrc: 'http://localhost:8080/sample.mp4'
    }
  },
  components: {
    VideoPlayer
  }
}
</script>
