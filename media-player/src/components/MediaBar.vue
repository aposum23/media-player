<template>
  <div class="media-bar">
    <img :src="mediaPhoto"/>
    <div class="media-descr">
      <h2>{{mediaName}}</h2>
      <h3>{{mediaAuthor}}</h3>
    </div>
    <figure>
      <audio controls src="" autoplay id="audioPlayer" @ended="playNextAudio"></audio>
    </figure>
  </div>
</template>

<script>
export default {
  name: 'MediaBar',
  props:[
    'mediaList',
  ],
  data(){
    return {
      mediaName: '',
      mediaAuthor: '',
      mediaPhoto: '',
      currentAudioId: 0,
      startFrom: 'start',
    }
  },
  methods: {
    playAudioFile(id, direction){
      let file = null;
      let fileId = id;
      console.log(fileId);
      if (direction === 'start'){
        console.log(fileId);
        file = this.mediaList[fileId].file;
      }
      else if (direction === 'end'){
        fileId = this.mediaList.length - 1;
        console.log(fileId);
        file = this.mediaList[fileId].file;
      }
      let player = document.getElementById('audioPlayer');
      const fileUrl = URL.createObjectURL(file);
      player.src = fileUrl;
      this.startFrom = direction;
      this.mediaName = this.mediaList[fileId].name;
      this.mediaAuthor = this.mediaList[fileId].author;
      this.mediaPhoto = this.mediaList[fileId].image;
      this.currentAudioId = fileId;
      player.play();
    },

    playNextAudio(){
      if (this.startFrom === 'start'){
        this.currentAudioId += 1;
      }
      else if (this.startFrom === 'end'){
        this.currentAudioId -= 1;
      }
      const file = this.mediaList[this.currentAudioId].file;
      let player = document.getElementById('audioPlayer');
      const fileUrl = URL.createObjectURL(file);
      this.mediaName = this.mediaList[this.currentAudioId].name;
      this.mediaAuthor = this.mediaList[this.currentAudioId].author;
      this.mediaPhoto = this.mediaList[this.currentAudioId].image;
      player.src = fileUrl;
      console.log(fileUrl);
      player.play();
    }
  }
}
</script>


<style lang="scss" scoped>
.media-bar{
  z-index: 10;
  display:inline-flex;
  position:fixed;
  bottom: 0px;
  width: 100%;
  border-top: 1px solid #000;
  background-color: rgb(254, 255, 203);

  & figure{
    margin-left: auto;
    display:inline-flex;
    & audio{
      width: 67em;
      margin: auto 0px;
    }
  }

  .media-descr {
    margin: auto 0px;
  }

  & img{
    width: 80px;
    height: 80px;
    margin: auto 1em;
  }

  & h2 {
    font-size: 18px;
  }

  & h3 {
    font-size: 14px;
  }
}
</style>
