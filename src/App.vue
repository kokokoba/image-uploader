<template>
  <ImageUploaderComplete/>
  <ImageUploader/>
  <Progress/>
</template>

<script>
import ImageUploader from './components/ImageUploader.vue'
import Progress from './components/Progress.vue'
import ImageUploaderComplete from './components/ImageUploaderComplete.vue'

export default {
  name: 'App',
  components: {
    ImageUploader,
    Progress,
    ImageUploaderComplete
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
</style>
