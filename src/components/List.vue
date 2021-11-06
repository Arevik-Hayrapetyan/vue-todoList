<template>
  <div class="wrapper">
    <div class="container">
      <div class="input-cnt">
        <input
          type="text"
          placeholder="What needs to be done?"
          class="text-input"
          v-model="inputValue"
        />
        <input type="submit" value="+" class="add-button" @click="handleAdd" />
      </div>

      <div v-for="(item, index) in addList" :key="index" class="added-list">
        <div class="value-cnt">
          <input
            type="checkbox"
            :isChecked="item.isChecked"
            @click="handleChecker(index)"
          />
          <div style="text-decoration-line: ">
            {{ item.inputValue }}
          </div>
        </div>
        <div class="edit-delete">
          <span class="status-btn" @click="handleStatus(index)">{{
            item.status
          }}</span>

          <i class="far fa-edit edit-btn" @click="handleEdit(index)"></i>
          <i
            class="far fa-trash-alt delete-btn"
            @click="handleDelete(index)"
          ></i>
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
      isChecked: false,
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
            isChecked: this.isChecked,
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
    handleChecker(index) {
      if (this.addList[index].isChecked === false) {
        this.addList[index].isChecked = true;
      } else {
        this.addList[index].isChecked = false;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.font {
  width: 100%;
}
.wrapper {
  display: flex;
  justify-content: center;
}
.container {
  width: 300px;
  height: 300px;
}

.added-list {
  background-color: #e0ffff;
  height: 40px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  margin-top: 5px;
}
.added-list:hover {
  background-color: #f0fff0;
}
.add-button {
  height: 40px;
  width: 100px;
  color: white;
  background-color: #4682b4;
  border-radius: 4px;
  margin-left: 3px;
}
.text-input {
  width: 600px;
  padding: 12px 20px;
  display: inline-block;
  border: 1px solid #7fffd4;
  border-radius: 4px;
  box-sizing: border-box;
}
.input-cnt {
  display: flex;
}
.edit-btn {
  color: #4682b4;
  margin-left: 8px;
}
.delete-btn {
  color: #4682b4;
  margin-left: 2px;
}
.status-btn {
  cursor: pointer;
}
.value-cnt {
  margin-left: 0;
  display: flex;
}
.edit-delete {
  display: flex;
  justify-content: space-between;
}
.isChecked {
  text-decoration: line-through;
}
</style>
