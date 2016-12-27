<template>
  <div id="app" class="col-md-8 col-md-offset-2 text-center">
    <h1 class="text-center">Simple Upload File with VUE 2.0</h1>
    <div class="container-fluid">
      <div class="text-left">
        <input type="file" @change="getFiles" name="file[]" id="file-upload" class="jaja-file-input" multiple/>
        <label for="file-upload"><span>Choose a file</span></label>
        <label id="file-upload-message"><span>No file been chosen.</span></label>
      </div>
      <preview-images :images="images" class="text-left"></preview-images>
    </div>
  </div>
</template>

<script>
  import previewImages from './components/previewImages.vue';
  import helper from './mixin/helper.vue';

  export default {
    name: 'app',
    components: {
      previewImages
    },
    mixins: [ helper ],
    data(){
      return {
        images: [],
      }
    },
    methods: {
      getFiles: function (e) {
        let files = e.target.files;
        let totalFiles = e.target.files.length;
        let images = this.images;
        for ( let image of files ) {
          let imgObj = {};

          // basic image details
          imgObj.name = image.name;
          imgObj.type = image.type;
          imgObj.size = Math.round(image.size / 1024) + 'KB';

          // get image temp path
          var reader = new FileReader();
          reader.onload = function (e) {
            imgObj.imgurl = e.target.result;
          };
          imgObj.imgurl = reader.readAsDataURL(image);

          images.push(imgObj);
        }
        this.showTotalFiles(this.images)

        return this.images = images
      },
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

  #file-upload-message{
    padding: 10px 20px;
    overflow: hidden;
  }

  .jaja-file-input{
    width: 0.1px;
    height: 0.1px;
    opacity: 0;
    overflow: hidden;
    position: absolute;
    z-index: -1;

    &+ label {
      /* 20px */
      font-weight: 700;
      white-space: nowrap;
      cursor: pointer;
      display: inline-block;
      overflow: hidden;
      padding: 10px 20px;
      color: #f1e5e6;
      background-color: #d3394c;

      &:hover{
         background-color: #722040;
      }
    }
  }
</style>