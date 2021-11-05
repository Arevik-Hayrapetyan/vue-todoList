<template>
  <div class="wrapper">
    <div class="container">
      <form class="todo-form">
        <input
          type="text"
          placeholder="todo..."
          class="text-input"
          v-model="inputValue"
        />
        <input type="submit" value="Add" class="add-button" />
      </form>
      <div class="added-list">{{ inputValue }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "List",
  props: {},
  data() {
    return {
      inputValue: "",
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
}
.container {
  width: 300px;
  height: 300px;
  display: flex;
  flex-wrap: wrap;
}
.todo-form {
  width: 300px;
  display: flex;
  justify-content: center;

  background-color: #b0b0b0;
}
.added-list {
  background-color: red;
  height: 50px;
  display: flex;
  align-items: center;
}
.add-button {
  height: 35px;
  width: 100px;
  color: white;
  background-color: blue;
}
.text-input {
  height: 30px;
  width: 400px;
}
</style>
