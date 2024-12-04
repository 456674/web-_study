<template>
  <div id="app">
    <el-container>
      <el-header>
        <h1>Vue ToDo List</h1>
      </el-header>
      <el-main>
        <el-card>
          <to-do-form @todo-added="addToDo"></to-do-form>
          <h2 id="list-summary">{{ listSummary }}</h2>
          <el-row>
            <el-col :span="24" v-for="item in ToDoItems" :key="item.id">
              <to-do-item
                  :label="item.label"
                  :done="item.done"
                  :id="item.id"
                  @checkbox-changed="updateDoneStatus(item.id, $event)"
              ></to-do-item>
            </el-col>
          </el-row>
        </el-card>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import ToDoForm from './components/ToDoForm.vue';
import ToDoItem from './components/ToDoItem.vue';

export default {
  components: {
    ToDoForm,
    ToDoItem
  },
  data() {
    return {
      ToDoItems: [
        {id: 1, label: "Learn Vue", done: false},
        {id: 2, label: "Build a Todo App", done: false},
        {id: 3, label: "Master JavaScript", done: false}
      ]
    };
  },
  computed: {
    listSummary() {
      const numberFinishedItems = this.ToDoItems.filter(item => item.done).length;
      return `${numberFinishedItems} out of ${this.ToDoItems.length} items completed`;
    }
  },
  methods: {
    addToDo(label) {
      this.ToDoItems.push({
        id: Date.now(),
        label: label,
        done: false
      });
    },
    updateDoneStatus(toDoId, done) {
      const toDoToUpdate = this.ToDoItems.find(item => item.id === toDoId);
      toDoToUpdate.done = done;
    }
  }
};
</script>

<style>
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
}
</style>
