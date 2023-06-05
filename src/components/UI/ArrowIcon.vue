<template>
    <button class="arrow" @click="addtodo">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="23.828"
            height="14.769"
          >
            <path
              d="m13.616 2.828 2.585 2.586H0v4h16.143l-2.527 2.526 2.828 2.829 7.384-7.384L16.444 0l-2.828 2.828z"
            />
          </svg>
        </button>
</template>
<script>
export default{
    methods:{
        addtodo(){
            this.$emit('addtodo')
        }
    }
}</script>