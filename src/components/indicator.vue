<template>
  <div :class="['string-fret-indicator', inScale && 'inScale']">
    {{ note }}
  </div>
</template>

<script>
export default {
  props: {
    note: String,
    inScale: Boolean,
  },
};
</script>

<style>
.string-fret-indicator {
  --size: 15px;
  font-size: 16px;
  font-family: sans-serif;
  font-weight: bold;
  display: inline-flex;
  background: white;
  border-radius: var(--size);
  height: var(--size);
  width: var(--size);
  padding: 5px;
  border: 1px solid black;
  text-align: center;
  justify-content: center;
  align-items: center;
}
.string-fret-indicator.inScale {
  background: #9aff8f;
}
</style>
