<template>
  <div id="app" class="col-md-8 col-md-offset-2 text-center">
    <h1 class="text-center">Simple Upload File with VUE 2.0</h1>
    <div class="container">
      <input type="file" multiple @change="getFiles" class="jaja-file-input">
      <preview-images :images="images" class="text-left"></preview-images>
    </div>
  </div>
</template>

<script>
  import previewImages from './components/previewImages.vue'

  export default {
    name: 'app',
    components: {
      previewImages
    },
    data(){
      return {
        images: []
      }
    },
    methods: {
      getFiles: function ( e ) {
        let files = e.target.files;
        let images = this.images;
        for ( let image of files ) {
          let imgObj = {};

          // basic image details
          imgObj.name = image.name;
          imgObj.type = image.type;
          imgObj.size = Math.round ( image.size / 1024 ) + 'KB';

          // get image temp path
          var reader = new FileReader ();
          reader.onload = function (e) {
            imgObj.imgurl = e.target.result;
          };
          imgObj.imgurl = reader.readAsDataURL ( image );

          images.push ( imgObj );
        }

        return this.images = images
      }
    }
  }
</script>

<style lang="scss">
  $icon-font-path: "~bootstrap-sass/assets/fonts/bootstrap/";
  @import "node_modules/bootstrap-sass/assets/stylesheets/_bootstrap.scss";

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  h1{
    margin-bottom: 30px;
  }

  .text-left {
    text-align: left;
  }
</style>
