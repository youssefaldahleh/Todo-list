<template>
  <error-card v-if="inputIsInvalid" @close="confirmError">
    <template #default>
      <p>Input Value Is Invalid</p>
      <p>Make Sure You Enter At Least A Few Characters</p>
    </template>
  </error-card>
  <div class="overray"></div>
  <base-card style="max-width: 25rem" class="test">
    <header>
      <h3>Task Detail</h3>
      <button @click="closemodel">X</button>
    </header>
    <div class="todo">
      <div class="text">
        <p v-show="inputSelected === false">{{ text }}</p>
        <input
          v-show="inputSelected"
          class="modelinput"
          type="text"
          :value="text"
          ref="EditingTodoText"
          :id="id"
        />
        <edit-icon @pargClicked="pargClicked"></edit-icon>
      </div>
      <button>!!!!priorty</button>
    </div>
    <!-- <priority-list @newpriorty="newpriorty" ></priority-list> -->
    <priority-list v-model="prioritySelcted"></priority-list>
    <div class="footer">
      <button @click="closemodel" class="close">CLOSE</button>
      <button @click="SubmitData" class="save">SAVE CHANGES</button>
    </div>
  </base-card>
</template>
<script>
import EditIcon from "../UI/EditIcon.vue";
import PriorityList from "@/components/Todolist/PriorityList.vue";
import ErrorCard from "../UI/ErrorCard.vue";
import BaseCard from "../UI/BaseCard.vue";
export default {
  props: {
    text: String,
    id: Number,
    todolist: Object,
    date: Date,
    todo: Object,
  },
  created() {
    this.editableTodo = {...this.todo}
  },
  data() {
    return {
      // prioritySelcted: "none",
      prioritySelcted:null,
      pargSelected: false,
      inputSelected: false,
      inputIsInvalid: false,
      editableTodo: null,
    };
  },
  components: {
    BaseCard,
    ErrorCard,
    PriorityList,
    EditIcon,
  },
  methods: {
    pargClicked() {
      this.inputSelected = true;
    },
    SubmitData() {
      const enteredTodoText = this.$refs.EditingTodoText.value;
      if (enteredTodoText.trim() === "") {
        this.inputIsInvalid = true;
        return;
      }
      const newToDoObj = {
        id: this.id,
        text: enteredTodoText,
        priorty: this.prioritySelcted,
        date: this.date,
        action: false,
      };
      this.$emit("editData", newToDoObj, this.id);
      console.log(this.prioritySelcted);
      console.log(newToDoObj);
    },
    newpriorty(priorty) {
      this.prioritySelcted = priorty;
      // console.log(priorty);
    },
    closemodel() {
      this.$emit("closemodel");
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
};
</script>
<style>
.overray {
  position: absolute;
  background-color: #0000004d;
  width: 100%;
  height: 100%;
  top: 0;
}
header {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #ddd;
}
header h3 {
  font-weight: normal;
  font-size: 25px;
}
header button {
  border: none;
  background-color: white;
  font-weight: normal;
  color: #ddd;
}
.todo {
  border-bottom: 1px solid #ddd;
  height: 150px;
}
.todo button {
  margin-top: 80px;
  width: 100%;
  border: none;
  border-radius: 4px;
  padding: 10px;
  color: blueviolet;
  background-color: #fff;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}
.text {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

svg {
  max-width: 20px;
  max-height: 20px;
}
.footer {
  margin-top: 10px;
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}
.footer button {
  border: none;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(255, 255, 255, 0.15);
  padding: 10px;
}
.save {
  color: white;
  background-color: blueviolet;
}
.modelinput {
  outline-style: none;
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: none;
  border-bottom: 2px solid powderblue;
}
.inputdisplay {
  visibility: hidden;
}
.pargdispaly {
  visibility: hidden;
}
</style>
