<script>
// give each todo a unique id
let id = 0;

export default {
  data() {
    return {
      newTodo: "",
      todos: [{ id: id++, text: "To Do list", isupdate: false }],
    };
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, isupdate: false });
      this.newTodo = "";

      let id = 0;

      this.todos.forEach((t) => {
        t.id = id++;
      });
    },
    removeTodo(todo) {
      this.todos = this.todos.filter(function (t) {
        return t !== todo;

        //   this.todos = this.todos.filter((t) => {
        //   console.log(todo, t);
        //   return t !== todo;
        // });
      });

      let id = 0;

      this.todos.forEach((t) => {
        t.id = id++;
      });
    },
    updateTodo(todo) {
      // this.update_flag = !this.update_flag;
      todo.isupdate = !todo.isupdate;

      if (todo.isupdate == false) {
        todo.text = this.$refs.el_update[todo.id].value;
      }
      // todo.text = this.$refs.el_update.value;
    },
  },
};
</script>

<template>
  <div>
    <div class="main">
      <div class="title">To Do List</div>
      <form @submit.prevent="addTodo" class="input">
        <input
          v-model="newTodo"
          placeholder="해야할 일을 입력해주세요."
          class="input_form"
        />
        <button class="input_button">+</button>
      </form>

      <ul class="items">
        <li v-for="todo in todos" :key="todo.id" class="item">
          <span class="point">●</span>&nbsp;&nbsp;
          <span v-if="!todo.isupdate">{{ todo.text }}</span>
          <input
            type="text"
            v-show="todo.isupdate"
            v-bind:value="todo.text"
            ref="el_update"
          />
          <button @click="updateTodo(todo)" class="update_button">수정</button>
          <button @click="removeTodo(todo)" class="remove_button">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  margin-top: 100px;
  width: 100%;
  height: 100%;
  min-height: 500px;
  max-width: 600px;
  border: black 2px solid;
  border-radius: 10px;
  background-color: #fafafa;
}
.title {
  font-size: 50px;
  margin: 10px;
  border-radius: 10px;
  background-color: lightcoral;
  color: whitesmoke;
}

.input {
  display: flex;
  justify-content: center;
}

.point {
  font-size: 13px;
  color: lightcoral;
}

.input_form {
  width: 100%;
  max-width: 500px;
  height: 100%;
  min-height: 25px;
  text-align: center;
  outline: none;
  color: transparent;
  text-shadow: 0 0 0 black;
}

.input_button {
  width: 100%;
  max-width: 30px;
  height: 100%;
  min-height: 30px;
  background-color: gray;
  color: white;
  font-size: 20px;
  border: none;
  border-radius: 5px;
  margin-left: 5px;
}

.items {
  display: flex;
  flex-direction: column;
  margin: 5px;
  color: black;
  font-size: 14px;
}

.item {
  display: flex;
  justify-content: flex-start;
  margin: 3px;
  margin-right: 50px;
  color: gray;
}

.remove_button {
  width: 100%;
  max-width: 20px;
  height: 100%;
  min-height: 20px;
  background-color: gray;
  color: white;
  font-size: 12px;
  border: none;
  border-radius: 5px;
  margin-left: 5px;
}

.update_button {
  width: 100%;
  max-width: 40px;
  height: 100%;
  min-height: 20px;
  background-color: gray;
  color: white;
  font-size: 12px;
  border: none;
  border-radius: 5px;
  margin-left: 15px;
}
</style>
