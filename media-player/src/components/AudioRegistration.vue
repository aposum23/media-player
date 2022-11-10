<template>
  <div class="audio-registration">
    <div class="audio-name">
      <label for="audio_name">Название песни:</label>
      <input type="text" name="audio_name" v-model="name"/>
    </div>
    <div class="audio-author">
      <label for="audio_author">Автор песни:</label>
      <input type="text" name="audio_author" v-model="author"/>
    </div>
    <div class="image-upload">
      <label for="audio_image">Добавте картинку для песни (Необязательно): </label>
      <input type="file" id="image" name="audio_image" accept=".jpg .png .svg"/>
    </div>
    <input class="save-button" type="button" value="Сохранить" @click="saveInformationAboutAudio()"/>
  </div>
</template>

<script>
export default {
  name: 'AudioRegistration',
  data(){
    return {
      name: null,
      author: null,
    }
  },
  methods: {
    saveInformationAboutAudio(){
      const input = document.getElementById('image');
      this.$emit('aboutAudio', {name: this.name, author: this.author, image: input.files[0]||require('@/assets/emptyAudio.svg')})
      this.name = null;
      this.author = null;
    }
  }
}
</script>


<style lang="scss" scoped>
.audio-registration {
  z-index: 8;
  margin: auto;
  width: 40em;
  height: 12em;
  background-color: rgb(254, 255, 203);
  border: 1px solid #000;

  .audio-name, .audio-author {
    width: 35em;
    margin-left: 10px;
    & input {
      margin: 10px auto 10px 10px; 
      width: 25em;
    }
  }

  .image-upload {
    width: 35em;
    margin-left: 10px;

    & input {
      margin: 10px auto 10px 10px; 
      width: 8.6em;
    }
  }

  .save-button {
    width: 38em;
    margin: 2em 4.5em;
  }
}
</style>
