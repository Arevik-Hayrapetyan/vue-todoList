<template>
  <div class="wrapper">
    <div class="container">
      <h3>TODOLIST</h3>
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
          <input type="checkbox" @click="handleChecker(index)" />
          <label
            v-bind:style="[
              item.isChecked
                ? { 'text-decoration': 'line-through' }
                : { 'text-decoration': 'none' },
            ]"
            >{{ item.inputValue }}</label
          >
        </div>
        <div class="edit-delete">
          <i
            v-bind:style="[
              item.isEditMode ? { color: '#4682b4' } : { color: '#bebebe' },
            ]"
            class="fas fa-pen edit-btn"
            @click="handleEdit(index)"
          ></i>
          <i
            class="fas fa-backspace delete-btn"
            @click="handleDelete(index)"
          ></i>
        </div>
      </div>

      <div class="remove-cnt">
        <div class="listdone-info" v-bind:style="{}">
          {{ filteredDoneList.length }} of {{ addList.length }} done
        </div>
        <button class="remove-btn" @click="handleRemove(item)">
          Remove checked X
        </button>
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
      isEditMode: false,
      isChecked: false,
      editedTask: null,
      index: Math.random(),
      inputValue: "",
      addList: [],
      filteredDoneList: [],
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
            isEditMode: this.isEditMode,
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
      this.addList[index].isEditMode = true;
      this.inputValue = this.addList[index].inputValue;
      this.editedTask = index;
    },

    handleChecker(index) {
      if (this.addList[index].isChecked === false) {
        this.addList[index].isChecked = true;
      } else {
        this.addList[index].isChecked = false;
      }
      this.filteredDoneList = this.addList.filter(
        (el) => el.isChecked === true
      );
    },
    handleRemove() {
      this.addList = this.addList.filter((el) => el.isChecked === false);
      this.filteredDoneList.length = 0;
      console.log(this.addList);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  display: flex;
  justify-content: center;
  font-weight: bold;
  font-size: 30px;
  margin-bottom: 5px;
}
.wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
}
.container {
  width: 500px;
  height: 500px;
  background-color: white;
  padding-left: 50px;
  padding-right: 50px;
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
  width: 80px;
  color: white;
  background-color: #4682b4;

  margin-left: 3px;
}
.text-input {
  width: 600px;
  padding: 12px 20px;
  display: flex;
  border: 1px solid #00ced1;
  box-sizing: border-box;
  justify-content: center;
}
.input-cnt {
  display: flex;
}
.edit-btn {
  margin-left: 8px;
  cursor: pointer;
}
.delete-btn {
  color: #bebebe;
  margin-left: 5px;
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
.remove-btn {
  height: 30px;
  width: 150px;
  color: white;
  background-color: #4682b4;
}
.remove-cnt {
  margin-top: 8px;
  display: flex;
  justify-content: space-between;
}
.listdone-info {
  height: 30px;
  width: 150px;
  border: 1px solid #bebebe;
  display: flex;
  align-items: center;
  position: relative;
  z-index: 1;
}
.listdone-info:before {
  position: absolute;
  z-index: -1;
  top: 0;
  left: 0;
  width: 60%;
  height: 100%;
  content: "";
  background-color: #7cfc00;
}
@media (max-width: 400px) {
  .input-cnt {
    width: 400px;
  }
}
</style>
