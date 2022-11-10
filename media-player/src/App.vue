<template>
  <div class="window">
    <MediaBar ref="mediaBar" :mediaList="mediaList"/>
    <FiltersBlock @loadAudio="addAudioInList" @startAudioFromEnd="startAudioFromEnd" @mixAudio="mixAndStartAudio" :media="mediaList"/>
    <TopBar/>
    <div class="media-list">
      <MediaListElement v-for="elem in mediaList" :media="elem" :key="elem.mediaName" @startPlayFrom="startAudio"/>
    </div>
    <AudioRegistration v-show="showAudioRegistration" @aboutAudio="saveAudioInformation"/>
  </div>
</template>

<script>
import TopBar from './components/TopBar.vue';
import MediaBar from './components/MediaBar.vue';
import MediaListElement from './components/MediaListElement.vue';
import FiltersBlock from './components/FiltersBlock.vue';
import AudioRegistration from './components/AudioRegistration.vue';

export default {
  name: 'App',
  data(){
    return {
      mediaList: [],
      lastAudioId: null,
      showAudioRegistration: false,
    }
  },
  components: {
    TopBar,
    MediaBar,
    MediaListElement,
    FiltersBlock,
    AudioRegistration,
  },
  methods: {
    addAudioInList(files){
      this.showAudioRegistration = !this.showAudioRegistration;
      let id = this.mediaList.length;
      for (let file of files){
        this.mediaList.push({id: id, file: file});
        this.lastAudioId = id;
        id += 1;
      }
    },

    saveAudioInformation(data){
      const id = this.lastAudioId;
      this.mediaList[id]['name'] = data.name;
      this.mediaList[id]['author'] = data.author;
      this.mediaList[id]['image'] = data.image;
      this.showAudioRegistration = !this.showAudioRegistration;
    },

    startAudio(data, direction='start'){
      let id = data.audioId || 0;
      const mediaBar = this.$refs.mediaBar;
      mediaBar.playAudioFile(id, direction);
    },

    startAudioFromEnd(){
      const mediaBar = this.$refs.mediaBar;
      mediaBar.playAudioFile(0, 'end');
    },

    mixAndStartAudio(){
      const mediaBar = this.$refs.mediaBar;
      this.mediaList = this.mixArr(this.mediaList);
      mediaBar.playAudioFile(0, 'start');
    },

    mixArr(arr){
      return arr.map(i=>[Math.random(), i]).sort().map(i=>i[1])
    },
  },
}
</script>

<style>
body{
  margin: 0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>

<style lang="scss" scoped>
.media-list{
  z-index: 1;
  margin: 5em 20em 5em 2em;
}
</style>