<template>
  <div class="wrapper">
    <div class="container">
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

      <div v-for="(item, index) in addList" :key="index" class="added-list">
        <div>{{ item.inputValue }}</div>
        <div class="edit-delete">
          <span class="status-btn" @click="handleStatus(index)">{{
            item.status
          }}</span>
          <button class="edit-btn" @click="handleEdit(index)">Edit</button>
          <button class="delete-btn" @click="handleDelete(index)">
            Delete
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "List",
  props: {},
  data() {
    return {
      editedTask: null,
      index: Math.random(),
      inputValue: "",
      status: "todo",
      addList: [],
    };
  },
  methods: {
    handleAdd() {
      if (this.inputValue !== "") {
        if (this.editedTask === null) {
          this.addList.push({
            index: this.index,
            inputValue: this.inputValue,
            editedTask: this.editedTask,
            status: this.status,
          });
        } else {
          this.addList[this.editedTask].inputValue = this.inputValue;
          this.editedTask = null;
        }
        this.inputValue = "";
      }
    },

    handleDelete(index) {
      this.addList.splice(index, 1);
    },
    handleEdit(index) {
      this.inputValue = this.addList[index].inputValue;
      this.editedTask = index;
    },
    handleStatus(index) {
      if (this.addList[index].status === "todo") {
        this.addList[index].status = "in-progress";
      } else if (this.addList[index].status === "in-progress") {
        this.addList[index].status = "ended todo";
      } else {
        this.addList[index].status = "todo";
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
}
.todo-form {
}
.added-list {
  background-color: #b0b0b0;
  height: 40px;
  display: flex;
  flex-direction: row;
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
.status-btn {
  cursor: pointer;
}
</style>
