<template>
  <div class="filters-block">
    <div class="section-mix">
      <img src="@/assets/mix-arrows.svg"/>
      <p @click="mixAudio()">Перемешать</p>
    </div>
    <div class="section-from-end">
      <img src="@/assets/arrow.svg"/>
      <p @click="startFromEnd()">Воспроизвести с конца</p>
    </div>
    <div class="section-add-file">
      <img src="@/assets/add.svg"/>
      <label for="file_input">Выбрать файл</label>
      <input @change="loadFile()" type="file" id="file_input" name="file_input" accept=".mp3" style="display: none;" multiple/>
    </div>
    <div class="section-add-file">
      <img src="@/assets/playlists.svg"/>
      <p>Плейлисты других</p>
    </div>
    <div class="drop-zone" @drop.prevent="getDropFile" @drag.prevent="getDropFile">
      <form ref="fileform">
        <p>Перетащите файлы сюда</p>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FiltersBlock',
  data(){
    return {
    }
  },
  calculated: {
  },
  methods: {
    loadFile(){
      const input = document.getElementById('file_input');
      this.$emit('loadAudio', input.files);
    },

    startFromEnd(){
      this.$emit('startAudioFromEnd');
    },
    
    mixAudio(){
      this.$emit('mixAudio');
    },

    getDropFile(e){
      const files = e.dataTransfer.files;
      this.$emit('loadAudio', files);
    }
  },
  mounted(){
    ['drag', 'dragstart', 'dragend', 'dragover', 'dragenter', 'dragleave', 'drop'].forEach( function( evt ) {
      document.body.addEventListener(evt, function(e){
        e.preventDefault();
        e.stopPropagation();
      });
    });
  },
}
</script>


<style lang="scss" scoped>
.filters-block {
  position: fixed;
  right:0px;
  width: 17em;
  height: 40em;
  border: 1px solid #000;
  margin-top: 70px;
  padding-top: 15px;
  background-color: rgb(254, 255, 203);

  .section-add-file, .section-from-end, .section-mix{
    display: inline-flex;
    margin-top: 10px;
    width: 100%;
  }

  .drop-zone {
    width: 80%;
    height: 100px;
    margin: 10px auto;
    border: 1px solid #000;

    & p {
      padding: 10px;
    }
  }

  & p {
    margin: auto 5px auto 0px;
  }

  & label {
    margin: auto 5px auto 0px;
  }

  & img {
    width: 15px;
    height: 15px;
    margin: 10px;
  }
}
</style>
