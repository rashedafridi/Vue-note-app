<template>
  <button :class="mode">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ['mode']
}
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #df5900;
  border: 1px solid #e7c3ff;
  color: white;
  cursor: pointer;
  border-radius: 10px;
}

button:hover,
button:active {
  background-color: #a02000;
  border-color: #dd726b;
}

.flat {
  background-color: transparent;
  color: #610b00;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #fb834b;
  color: azure;

}
</style>