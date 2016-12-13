<template>
  <div id="preview-images">
    <div is="image-thumbnail"
         v-for="(image, index) in images"
         :image="image"
         :style="{ backgroundImage: 'url(' + image.imgurl + ')' }"
         @remove="images.splice(index, 1)">
    </div>
  </div>
</template>

<script>
  import ImageThumbnail from './ImageThumbnail.vue'

  export default {
    name: 'previewImages',
    props: [ 'images' ],
    components: {
      ImageThumbnail
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>

</style>
