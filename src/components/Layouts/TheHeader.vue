<template>
  <header>
    <h2>{{ title }}</h2>
  </header>
</template>
<script>
export default {
    props:{
        title:String
    }
};
</script>
<style scoped>
header {
  width: 100%;
  display: flex;
  align-items: top;
  justify-content: center;
}
h2 {
  color:white;  
  text-align: center;
  margin-top: 20px;
}
</style>
