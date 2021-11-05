<template>
  <div class="wrapper">
    <div class="container">
      <form class="todo-form">
        <div class="input-cnt">
          <input
            type="text"
            placeholder="todo..."
            class="text-input"
            v-model="inputValue"
          />
          <input
            type="submit"
            value="Add"
            class="add-button"
            @click="handleAdd"
          />
        </div>

        <div v-for="item in addList" :key="item.id" class="added-list">
          <li>{{ item.inputValue }}</li>
          <div class="edit-delete">
            <button class="edit-btn">Edit</button>
            <button class="delete-btn">Delete</button>
          </div>
        </div>
      </form>
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
      addList: [{ inputValue: "hey", id: Math.random() }],
    };
  },
  methods: {
    handleAdd() {
      console.log("arev");
      if (this.inputValue !== "") {
        return {
          addList: [
            ...this.addList,
            {
              id: Math.random(),
              inputValue: this.inputValue,
              isChecked: false,
              isEditMode: false,
            },
          ],
          inputValue: "",
        };
      }
    },
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
}
.added-list {
  background-color: #b0b0b0;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.add-button {
  height: 35px;
  width: 100px;
  color: white;
  background-color: blue;
}
.text-input {
  height: 30px;
  width: 200px;
}
.input-cnt {
  display: flex;
}
.edit-btn {
  color: white;
  background-color: blue;
}
.delete-btn {
  color: white;
  background-color: red;
}
</style>
