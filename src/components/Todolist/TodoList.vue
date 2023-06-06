<template>
  <error-card v-if="inputIsInvalid" @close="confirmError">
    <template #default>
      <p>Input Value Is Invalid</p>
      <p>Make Sure You Enter At Least A Few Characters</p>
    </template>
  </error-card>

  <base-card>
    <div class="todo-list">
      <header>
        <p>TODO-LIST</p>
      </header>
      <div class="todo-status">
        <p class="total">ToTAL:{{ todolist.length }}</p>
        <p class="success">SUCCESS:{{ completedCount }}</p>
        <p class="pending">PENDING:{{ todolist.length - completedCount }}</p>
      </div>
      <div class="input-todo">
        <input
          type="text"
          placeholder="Enter New To Do"
          @keyup.enter="addtodo"
          v-model.trim="enteredtodotext"
        />
        <arrow-icon @addtodo="addtodo"></arrow-icon>
      </div>
      <table>
        <tr v-for="todo in todolist" :key="todo.text" :id="todo.id">
          <td>
            <button @click="clickrow(todo)">
              {{ todo.text }}
            </button>
          </td>
          <td>{{ todo.priorty ? `${priorities[todo.priorty]} Priority` : '' }}</td>
          <td>{{ todo.date }}</td>
          <td>
            <input
              type="checkbox"
              name="sucsses"
              :value="id"
              :id="todo.id"
              v-model="todo.action"
            />
          </td>
          <td>
            <button @click="deletetodo(todo.id)">
              <clear-icon></clear-icon>
            </button>
          </td>
        </tr>
      </table>
      <div class="clearall">
        <button @click="clearall" class="">Clear All</button>
        <clear-icon @allClear="clearall"></clear-icon>
      </div>
    </div>
  </base-card>
  <edit-list
    v-if="displayModel === true"
    :text="displaytodotext"
    :id="id"
    :date="date"
    :todo="activeTodo"
    @editData="editData"
    @closemodel="closemodel"
  ></edit-list>
</template>
<script>
import ArrowIcon from "../UI/ArrowIcon.vue";
import ErrorCard from "../UI/ErrorCard.vue";
import BaseCard from "../UI/BaseCard.vue";
import EditList from "./EditList.vue";
import ClearIcon from "../UI/ClearIcon.vue";
import { priorities } from '../../helpers/enums';

export default {
  components: {
    BaseCard,
    EditList,
    ErrorCard,
    ArrowIcon,
    ClearIcon,
  },
  data() {
    return {
      inputIsInvalid: false,
      displayModel: false,
      enteredtodotext: "",
      displaytodotext: "",
      date: "",
      id: "",
      todolist: [
        {
          id: 1,
          text: "standup meeting",
          priorty: 1,
          date: new Date().toLocaleDateString("en-us", {
            month: "short",
            day: "numeric",
          }),
          action: false,
        },
        {
          id: 2,
          text: "Order pizza for Granny tonigth",
          priorty: 3,
          date: new Date().toLocaleDateString("en-us", {
            month: "short",
            day: "numeric",
          }),
          action: false,
        },
        {
          id: 3,
          text: "Desig ,Develop and Deploy Apps to Netlife Clierts",
          priorty: 2,
          date: new Date().toLocaleDateString("en-us", {
            month: "short",
            day: "numeric",
          }),
          action: false,
        },
      ],
      // new code
      activeTodo: null,
      priorities,
    };
  },

  computed: {
    completedCount() {
      return this.todolist.filter((todo) => todo.action).length;
    },
  },

  methods: {
    addtodo() {
      const date = new Date().toLocaleDateString("en-us", {
        month: "short",
        day: "numeric",
      });
      const newtodo = {
        id: this.todolist.length + 1,
        text: this.enteredtodotext,
        priorty: 4,
        date: date,
        action: false,
      };
      if (this.enteredtodotext === "") {
        this.inputIsInvalid = true;
        return;
      } else {
        this.todolist.push(newtodo);
      }
      this.enteredtodotext = "";
     
    },

    deletetodo(itemid) {
      this.todolist = this.todolist.filter((item) => item.id !== itemid);
    },
    clearall() {
      this.todolist = [];
    },
    clickrow(todo) {
      this.id =todo.id;
      this.displaytodotext =todo.text;
      this.date = todo.date;
      this.displayModel = true;

      // new code
      this.activeTodo = { ...todo };
      console.log(this.activeTodo);
    },

    setEditcomp() {
      this.displayModel = !this.displayModel;
    },
    editData(newEditTodo, editId) {
      const newTodo = this.todolist.findIndex((todo) => todo.id === editId);
      this.todolist[newTodo] = newEditTodo;
      console.log(newTodo);
      console.log(newEditTodo);
      this.displayModel = false;
    },
    closemodel() {
      this.displayModel = false;
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
};
</script>
<style scoped>
.clearall {
  display: flex;
  max-width: 80px;
  justify-content: space-around;
  align-items: end;
  margin-top: 100px;
}
.clearall button {
  border: none;
  background-color: white;
  cursor: pointer;
}
.clearall svg {
  max-width: 20px;
  max-height: 20px;
  cursor: pointer;
}
table {
  width: 100%;
}
table td {
  padding-top: 20px;
}
table td button {
  border: none;
  background-color: white;
}
table td svg {
  width: 15px;
  cursor: pointer;
}
.todo-list {
  background-color: white;
}
header {
  text-align: left;
  padding: 20px;
  font-size: 20px;
}
.todo-status {
  display: flex;
  justify-content: space-around;
  margin-bottom: 30px;
}
.todo-status p {
  border-radius: 4px;
  padding: 3px;
}
.total {
  color: rgb(142, 80, 201);
  background-color: rgb(206, 183, 228);
}
.success {
  color: rgb(103, 170, 41);
  background-color: rgb(172, 228, 146);
}
.pending {
  color: rgb(233, 87, 87);
  background-color: rgb(230, 137, 137);
}
.input-todo {
  display: flex;
}
.arrow {
  border: none;
  cursor: pointer;
}
input {
  outline-style: none;
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: none;
  border-bottom: 2px solid powderblue;
}
</style>
