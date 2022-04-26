<template>
  <div>
    <input @click="addTag" class="tags-input" type="text" />
  </div>
</template>

<script>
export default {
  name: "tags-input",
  props: {
    addTag: {
      type: Function,
    },
  },
};
</script>

<style scoped>
.tags-input {
  margin: 10px;
  border: 0.7px solid lightgrey;
  border-top-style: hidden;
  border-right-style: hidden;
  border-left-style: hidden;
  border-bottom-style: ridge;
  width: 100%;
  height: 30px;
}
</style>
