<template>
  <base-card>
    <p>Set priorty of your task</p>
    <div>
      <label class="high">
        <input
          type="radio"
          name="priorty"
          v-model="priorty"
          value="3"
          @change="newpriorty('3')"
        />
        <p>!!!!</p>
        High</label
      >
    </div>
    <div>
      <label class="medium">
        <input
          type="radio"
          name="priorty"
          v-model="priorty"
          value="2"
          @change="newpriorty('2')"
        />
        <p>!!</p>
        Medium</label
      >
    </div>
    <div>
      <label class="low">
        <input
          type="radio"
          name="priorty"
          v-model="priorty"
          value="1"
          @change="newpriorty('1')"
        />
        <p>!</p>
        Low</label
      >
    </div>
    <div>
      <label class="noue">
        <input
          type="radio"
          name="priorty"
          v-model="priorty"
          value="4"
          @change="newpriorty('4')"
          checked="checked"
        />
        <p>!!!</p>
        Noue</label
      >
    </div>
  </base-card>
</template>
<script>
import BaseCard from "../UI/BaseCard.vue";
export default {
  props: {
    modelValue: {
      type: String,

    },
    oldPriority:{
      type:Object
    }
  },
  emits: ["update:modelValue"],
  data() {
    return {
      priorty: this.modelValue,
    };
  },

  components: {
    BaseCard,
  },
  methods: {
    newpriorty(priorty) {
      this.priorty = priorty;
      // console.log(priorty.target.value)
      this.$emit("update:modelValue", priorty);
      console.log(priorty);

      console.log(this.oldPriority);
    },
  },
};
</script>
<style scoped>
div {
  margin: 15px;
}
p {
  margin-left: 10px;
}
label p {
  display: inline;
  margin: 0 10px;
}
.high p {
  color: red;
}
.medium p {
  color: yellow;
}
.low p {
  color: blueviolet;
}
</style>
