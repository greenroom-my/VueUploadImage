<template>
  <div class="div-img"
       @mouseover="showWrapper(this)"
       @mouseleave="removeWrapper(this)">

    <div class="wrapper" :class="wrapper">
      <p class="cancel-btn text-right" @click="$emit('remove')">x</p>
      <p class="text-center img-title">
        {{image.name}}
      </p>
      <p class="text-center img-size">{{image.size}}</p>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'image-thumbnail',
    props: [ 'image' ],
    data(){
      return {
        wrapper: 'hidden'
      }
    },
    methods: {
      showWrapper: function ( e ) {
        this.wrapper = '';
      },
      removeWrapper: function ( e ) {
        this.wrapper = 'hidden';
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  .div-img {
    height: 150px;
    width: 150px;
    border-radius: 5px;
    float: left;
    margin: 10px;
    background: no-repeat center;
    background-size: cover;
  }

  .wrapper {
    position: relative;
    opacity: 0.9;
    width: 100%;
    height: 100%;
    border-radius: 5px;
    background-color: rgb(128, 128, 128);

    p{
      color: white;
      margin: 0 0;

      &.img-title{
        padding: 25px 20px;
        height: 90px;
        text-align: center;
        width:100%;
        word-break: break-all;
        word-wrap: break-word;

      }

      &.img-size{
        padding-top: 10px;
        height: 20px;
      }

      &.cancel-btn {
        padding: 2px 10px 4px 0px;
        font-size: 16px;
        cursor: pointer;
      }
    }
  }
</style>
