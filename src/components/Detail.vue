<template>
  <div class="detail">
    <div class="image">
      <img class="responsive" :src="trackDetails.album.images[0].url" />
    </div>
    <div class="">
      <label class="labelName"> {{ trackDetails.name }} </label>
    </div>
    <div class="">
      <label class="labelArtis">
        {{ trackDetails.artists[0].name }}
      </label>
    </div>
  </div>
</template>

<script >
export default {
  name: "Detail",
  props: {
    trackDetails: String,
  },

  setup() {},
};
</script>

<style scoped>
.detail {
  position: absolute;
  top: 50px;
  right: 0px;
  margin: 20px;
}
.responsive {
  width: 100%;
  height: auto;
}
</style>