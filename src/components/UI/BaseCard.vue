<template>
   
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
div {
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  margin: 2rem auto;
  max-width: 40rem;
  background-color: white;
}
.test {
  width: 24rem;
  position: absolute;
  top:8%;
  right:34%;
  z-index: 9;
}
</style>
