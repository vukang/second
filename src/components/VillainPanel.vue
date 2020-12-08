<template>
  <div class="villainContainer">
    <h3>Villain #1</h3>
    {{ villainC }}
  </div>
</template>

<script>
export default {
  props: ["villainC"],
  data() {
    return {};
  },
  methods: {},
  computed: {},
};
</script>

<style scoped>
.villainContainer {
  width: 200px;
  height: 100px;
  background-color: azure;
}
</style>