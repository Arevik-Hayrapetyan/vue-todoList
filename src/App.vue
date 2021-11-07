<template>
  <List class="list" />
</template>

<script>
import List from "./components/List.vue";

export default {
  name: "App",
  components: {
    List,
  },
};
</script>

<style scoped>
.list {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
