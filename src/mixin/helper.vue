<script>
  module.exports = {
    methods: {
      showTotalFiles: function (images) {
        let totalImages = images.length;
        let text = 'No file been chosen.';

        if ( totalImages >= 1 )
          text = totalImages + ' file total.';

        let label = document.getElementById("file-upload-message");
        label.querySelector('span').innerHTML = text;
      }
    }
  }
</script>