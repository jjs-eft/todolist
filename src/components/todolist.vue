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
      const modal = document.querySelector(".modal");
      const backdrop = document.querySelector(".backdrop");
      backdrop.classList.add("_on");
      modal.classList.add("_btn");

      todo.text = this.$refs.el_update[todo.id].value;
      // todo.text = this.$refs.el_update.value;
    },

    closeUpdate() {
      const modal = document.querySelector(".modal");
      const backdrop = document.querySelector(".backdrop");
      backdrop.classList.remove("_on");
      modal.classList.remove("_btn");
    },

    closeUpdatenoC() {
      const modal = document.querySelector(".modal");
      const backdrop = document.querySelector(".backdrop");
      backdrop.classList.remove("_on");
      modal.classList.remove("_btn");
    },
  },
};
</script>

<template>
  <div>
    <div class="modal">
      <div class="modal_content">
        <div class="div_clbtn">
          <div class="clbtn_cont">수정하기</div>
          <button @click="closeUpdatenoC()" class="close_button">X</button>
        </div>
        <input
          @keyup.enter="submit"
          type="text"
          ref="el_update"
          class="update_input"
        />
        <button @click="closeUpdate()" class="closebtn">수정 완료</button>
      </div>
    </div>
    <div @click="closeUpdatenoC()" class="backdrop"></div>
    <div class="main">
      <div class="title">To Do List</div>
      <form @submit.prevent="addTodo" class="input">
        <input
          @keyup.enter="submit"
          v-model="newTodo"
          placeholder="해야할 일을 입력해주세요."
          class="input_form"
        />
        <button class="input_button">+</button>
      </form>

      <ul class="items">
        <li v-for="todo in todos" :key="todo.id" class="item">
          <span class="point">●</span>&nbsp;&nbsp;
          <span>{{ todo.text }}</span>

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

.div_clbtn {
  width: 100%;
  background-color: red;
  display: flex;
  justify-content: space-between;
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
  margin: 0 auto;
}

.clbtn_cont {
  width: 100%;
  height: 100%;
  color: white;
  font-size: 20px;
  font-style: bold;
  margin-left: 40px;
}

.close_button {
  width: 100%;
  min-width: 30px;
  max-width: 40px;
  height: 100%;
  min-height: 30px;
  max-height: 30px;
  background-color: gray;
  color: white;
  font-size: 12px;
  border: none;
  border-top-right-radius: 6px;
}

.remove_button {
  width: 100%;
  max-width: 20px;
  height: 100%;
  min-height: 20px;
  max-height: 20px;
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

.modal {
  /* background-color: #aaaa; */
  display: none;
  justify-content: center;
  align-items: center;

  width: 350px;
  height: 350px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.modal._btn {
  display: flex;
  z-index: 1;
}

.modal_content {
  background-color: pink;
  width: 350px;
  height: 350px;
  position: fixed;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-end;
}

.closebtn {
  margin: 15px auto;
  width: 100%;
  max-width: 70px;
  height: 100%;
  max-height: 20px;
  background-color: gray;
  color: white;
  border: none;
  border-radius: 5px;
}

.update_input {
  width: 100%;
  max-width: 300px;
  height: 100%;
  max-height: 20px;
  outline: none;
  color: transparent;
  text-shadow: 0 0 0 black;
  margin: 0 auto;
  margin-top: 120px;
}

.backdrop {
  width: 100%;
  height: 100%;
  background-color: #aaaa;
  z-index: 0;
  display: none;
  position: fixed;
}

.backdrop._on {
  display: flex;
}
</style>
