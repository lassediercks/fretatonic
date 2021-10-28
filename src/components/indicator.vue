<template>
  <div
    :class="[
      'string-fret-indicator',
      inScale && 'inScale',
      inChord && 'inChord',
    ]"
  >
    {{ note }}
    <span
      v-show="showPosition"
      class="scalePosition"
      v-if="scalePosition !== 0"
    >
      {{ scalePosition }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    showPosition: Boolean,
    scalePosition: Number,
    note: String,
    inChord: Boolean,
    inScale: Boolean,
  },
};
</script>

<style>
.string-fret-indicator {
  position: relative;
  --size: 25px;
  font-size: 16px;
  font-weight: bold;
  display: inline-flex;
  background: white;
  border-radius: 10px;
  height: var(--size);
  width: var(--size);
  padding: 5px;
  border: 1px solid black;
  text-align: center;
  justify-content: center;
  align-items: center;
}
.scalePosition {
  position: absolute;
  font-size: 14px;
  bottom: 100%;
}
.string-fret-indicator.inScale {
  background: #68cbd8;
}
.string-fret-indicator.inChord {
  color: white;
  background: #640f3c;
}
</style>
