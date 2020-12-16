<template>
  <button
    class="close"
    aria-label="close"
  ></button>
</template>
<style scoped>
.close {
  position: relative;
  width: 1.5rem;
  height: 1.5rem;
  min-width: 1.5rem;
  border-radius: 0.75rem;
  cursor: pointer;
  background:rgba(10,10,10,.4);
  border: none;
  padding: 0;
  font-size: 0;
  text-align: center;
  outline: 0;
}
.close:before,
.close:after {
  content: '';
  position: absolute;
  width: 50%;
  height: 2px;
  left:50%;
  top: 50%;
  background: white;
  transform: translateX(-50%) translateY(-50%) rotate(45deg);
  transform-origin: center center;  
}
.close::after {
  height: 50%;
  width: 2px;
}
</style>