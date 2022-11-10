<template>
  <div class="media-list-element">
    <img :src="media.image" @mouseenter="showHidePlayButton"/>
    <img src="@/assets/playButton.svg" v-show="playButton" id="play" class="play-button" @mousedown="startAudio" @click="playAudioFile" @mouseup="deleteOpacityFromPlay" @mouseleave="showHidePlayButton"/>
    <div class="media-info">
      <h2>{{media.name}}</h2>
      <h3>{{media.author}}</h3>
    </div>
    <p>{{media.size}}</p>
  </div>
</template>

<script>
export default {
  name: 'MediaListElement',
  props: [
    'media',
  ],
  data(){
    return {
      playButton: false,
    }
  },
  methods: {
    showHidePlayButton(){
      this.playButton = !this.playButton;
    },

    startAudio(){
      let button = document.getElementById('play');
      button.style.opacity = 1;
    },

    deleteOpacityFromPlay(){
      let button = document.getElementById('play');
      button.style.opacity = 0.6;
    },

    playAudioFile(){
      this.$emit('startPlayFrom', {audioId: this.media.id});
    }
  }
}
</script>


<style lang="scss" scoped>
.media-list-element{
  display: inline-flex;
  width:100%;
  & img {
    width: 80px;
    height: 80px;
    margin: auto 5px;
  }

  .play-button{
    margin-left: -85px;
    opacity: 0.6;
  }
  .media-info {
    margin:auto 20px;
  }

  & h2 {
    font-size: 18px;
  }

  & h3 {
    font-size: 14px;
  }

  & p {
    margin: auto 0px auto auto
  }
}
</style>
