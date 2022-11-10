<template>
  <div class="top-bar">
    <h2>Media player</h2>
    <img :src="userImage"/>
  </div>
</template>

<script>
export default {
  name: 'TopBar',
  data(){
    return {
      userImage: require('@/assets/user.svg'),
    }
  },
  calculated: {
  },
  methods: {
  },
}
</script>


<style lang="scss" scoped>
.top-bar {
  display: inline-flex;
  width: 100%;
  background-color: rgb(254, 255, 203);
  border-bottom: 1px solid #000;

  & h2 {
    padding: 0px;
    margin: auto 20px;
  }

  & img {
    width: 50px;
    height: 50px;
    margin: auto 0px auto auto;
    padding: 10px 30px;
    border-radius: 90px;
  }
}
</style>
