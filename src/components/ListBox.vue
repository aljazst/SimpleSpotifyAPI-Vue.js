<template>
  <div class="list">
    <button
      v-for="list in listOfSongs"
      :key="list"
      v-on:click="buttonClicked($event)"
      :id="list.track.id"
    >
      {{ list.track.name }}
    </button>
  </div>
</template>

<script >
export default {
  name: "ListBox",
  data() {
    return { id: null };
  },
  props: {
    listOfSongs: [],
  },
  methods: {
    buttonClicked(event) {
      const targetId = event.currentTarget.id;
      this.$emit("buttonClicked", targetId);
      console.log("this button was clicked " + targetId);
    },
  },
};
</script>

<style scoped>
button {
  position: relative;
  justify-content: center;
  display: list-item;
  margin: 0 auto;
  margin-top: 3px;
  background-color: #fff;
  border-radius: 4px;
  border: 2px solid #e7e7e7;
  padding: 15px 32px;
  text-align: center;
  min-width: 330px;
}
button:hover {
  background-color: #f8f8f8;
}
</style>