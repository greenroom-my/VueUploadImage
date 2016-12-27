<template>
  <div id="preview-images">
    <div is="image-thumbnail"
         v-for="(image, index) in images"
         :image="image"
         :index="index"
         :removePreview="remove"
         :style="{ backgroundImage: 'url(' + image.imgurl + ')' }">
    </div>
  </div>
</template>

<script>
  import ImageThumbnail from './ImageThumbnail.vue';
  import helper from '../mixin/helper.vue';

  export default {
    name: 'previewImages',
    props: [ 'images' ],
    mixins: [ helper ],
    components: {
      ImageThumbnail
    },
    methods: {
      remove: function (index) {
        this.images.splice(index, 1);
        this.showTotalFiles(this.images);
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>

</style>
