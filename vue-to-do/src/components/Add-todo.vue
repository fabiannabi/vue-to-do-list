<template>
  <div class="toDo__container">
    <div class="toDo__title">
      <h1>TO DO LIST</h1>
    </div>
    <form @submit.prevent="AddNew" class="toDo__addNew">
      <input v-model="AddedTask" type="text" placeholder="Add new task" />
      <button type="submit" class="toDo__button--main">Add</button>
    </form>
    <div v-show="error" class="error">Please Add A To Do</div>
    <div class="toDo__display">
      <li :class="{done:toDo.done}" v-for="toDo in ToDos" :key="toDo.id">
        {{toDo.title}}
        <!--para saber si esta como true , se pone checked y se le asigna a que sera igual y para asegurar que buscara entre la data hay que hacer bind-->
        <input v-model="toDo.done" type="checkbox" class="checkbox" />
        <button @click="Remove(toDo)" class="remove">Remove</button>
      </li>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      error: false,
      done: false,
      AddedTask: "",
      ToDos: []
    };
  },

  methods: {
    AddNew: function() {
      if (this.AddedTask) {
        this.ToDos.push({ title: this.AddedTask, done: false });
        console.log(this.ToDos);
        this.AddedTask = "";
        this.error = false;
      } else {
        this.error = true;
      }
    },
    Remove(el) {
      //primero encontrarlo en el array, this. cada elemento agregado en el array index of elemento especifico
      const toDoIndex = this.ToDos.indexOf(el);
      console.log(toDoIndex);
      this.ToDos.splice(toDoIndex, 1);
    },
    removeAll() {
      this.ToDos.forEach(toDo => {
        toDo.done = true;
      });
    }
  }
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: rgb(200, 231, 221);
}

.toDo__container {
  margin: auto;
  width: 50%;
  text-align: center;
  padding-top: 1em;
}
.toDo__title {
  padding-bottom: 1em;
}

.toDo__display {
  text-decoration: none;
}
.toDo__display li {
  background-color: rgb(138, 151, 133);
  margin: 10px 10px;
  list-style: none;
  font-size: 1.5em;
  text-align: center;
  justify-content: space-evenly;
}

.done {
  text-decoration: line-through;
  color: green;
}
.remove {
  background-color: rgb(18, 87, 30);
  border-style: solid 10px rgb(68, 43, 43);
  font-size: 0.8em;
  color: white;
  text-decoration: none;
}
.error {
  font-size: 1.5em;
  padding-top: 1em;
}
.toDo__button--main {
  background-color: rgb(24, 153, 46);
  border-style: solid 10px rgb(68, 43, 43);
  font-size: 1.5em;
  border-radius: 10px;
  padding: 2px;
  color: white;
  text-decoration: none;
}
</style>
