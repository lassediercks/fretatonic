<template>
  <div class="fretboard">
    <div class="strings">
      <div
        class="string-wrap"
        v-for="(string, index) in [...Array(6)]"
        :key="`string-${index}`"
      >
        <div class="string-fret" v-for="fret in frets" :key="fret"></div>
        <div class="string"></div>
      </div>
    </div>
    <div class="frets">
      <div class="fret" v-for="(fret, index) in frets" :key="fret">
        <div class="dots">
          <template v-if="singleDotFrets.includes(index)">&#183;</template>
          <template v-if="index == 12">&#183;&#183;</template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const singleDotFrets = [3, 5, 7, 9, 15, 17, 19, 21];
export default {
  name: "App",
  components: {},
  data() {
    return {
      singleDotFrets,
      frets: 21,
    };
  },
};
</script>

<style>
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  padding: 0;
}
.fretboard {
  position: relative;
  width: 1200px;
  height: 200px;
}
.strings {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  left: 0;
  top: 0;
  bottom: 0;
  width: 100%;
}
.string-wrap {
  position: relative;
  width: 100%;
  height: 30px;
  display: flex;
  align-items: center;
}

.string {
  position: absolute;
  top: 50%;
  left: 0;
  width: 100%;
  display: flex;
  flex: 1;
  height: 2px;
  background: #000;
}

.frets {
  height: 100%;
  display: flex;
}

.fret {
  position: relative;
  font-size: 40px;
  height: 100%;
  width: 90px;
  border-right: 1px solid black;
}
.dots {
  position: absolute;
  top: 100%;
  display: flex;
  justify-content: center;
  width: 100%;
}
</style>
