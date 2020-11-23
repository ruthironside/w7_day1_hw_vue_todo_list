<template>
  <div id="app"> 
    <form v-on:submit.prevent="saveNewTask">
      <label for="new-task">Add a new task:</label>
      <input id="new-task" type="text" v-model="newTask"/>
      <input type="submit" value="Save new task">
      <label for="high">High</label>
      <input type="radio" id="high-priority" value="High Priority" v-model="priority"/>
      <label for="low">Low</label>
      <input type="radio" id="low-priority" value="Low Priority" v-model="priority"/>
    </form>

    <ul>
      <li v-for="(task, index) in tasks" :key="index" v-bind:class="task.isCompleted ? 'completed':'not-completed'">
      <span>{{task.name}}</span>
      <span>{{task.priority}}</span>
      <span v-if="task.isCompleted">Done!!</span>
      <button v-if="!task.isCompleted" v-on:click="taskDone(index)">Complete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data(){
    return {
      tasks: [
        {name: "Feed the dog", isCompleted: true, priority: "High Priority"},
        {name: "Water the plants", isCompleted: false, priority: "High Priority"},
        {name: "Clean the kitchen", isCompleted: true, priority: "Low Priority"}
      ],
      newTask: "",
      priority: ""
    }
  },
  methods: {
    saveNewTask: function() {
      this.tasks.push({
        name: this.newTask,
        isCompleted: false,
        priority: this.priority
      });
      this.newTask = "";
      this.priority = "";
    },
    taskDone: function(index) {
      this.tasks[index].isCompleted = true;
    }
  }
}
</script>

<style>
#app {
  width: 60%;
  margin: 0 auto;
  font-family: 'Lato', sans-serif;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

li {
  margin: 20px 0;
  padding: 10px;
  display: flex;
  justify-content: space-between;
}

li span {
  padding: 8px;
}

li button {
  background: #f2360c;
  color: #fff;
  border: none;
  padding: 10px;
  cursor: pointer;
}

li.completed {
  border: 2px solid #1a681e;
  color: #1a681e;
}

li.not-completed {
  border: 2px solid #f2360c;
}

input[type="text"] {
  padding: 10px;
  width: 50%;
  margin:5px;
}

button, input[type="submit"]{
  padding: 10px;
  background: #000;
  color: #fff;
  cursor: pointer;
  border: 1px solid #000;
}

</style>