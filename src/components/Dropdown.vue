<template>
  <div class="dropdown">
    <label>{{ label }}</label>
    <select v-on:change="onChengeDetected" v-model="selectedType">
      <option v-for="list in genreList" :key="list" :value="list.id">
        {{ list.name }}
      </option>
    </select>
  </div>
</template>

<script >
export default {
  name: "Dropdown",
  data() {
    return {
      selectedType: "",
    };
  },
  props: {
    label: String,
    genreList: Array,
    genreChange: String,
  },
  methods: {
    onChengeDetected() {
      this.$emit("valueChanged", this.selectedType);
    },
  },
};
</script>

<style scoped>
body {
  font-family: "Source Sans Pro", "Helvetica Neue", Arial, sans-serif;
  text-rendering: optimizelegibility;
  -moz-osx-font-smoothing: grayscale;
  -moz-text-size-adjust: none;
}

h1,
.muted {
  color: #2c3e5099;
}

h1 {
  font-size: 26px;
  font-weight: 600;
}

#dropdown {
  position: relative;
  display: inline-block;
  display: flex;
  justify-content: center;
}
label {
  text-align: left;
  line-height: 150%;
  font-size: 20px;
}

select {
  width: 100%;
  min-width: 15px;
  max-width: 300px;
  border-radius: 8px;
  border: 3px solid var(--select-border);
  padding: 0.25em 0.5em;
  margin-bottom: 33px;
  font-size: 1.25rem;
  cursor: pointer;
  line-height: inherit;
  background-color: #fff;
  background-image: linear-gradient(to top, #f9f9f9, #fff 33%);
  outline: none;

  box-shadow: 2px 2px 2px rgb(168, 168, 168);
}
</style>