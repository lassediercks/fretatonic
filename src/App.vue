<template>
  <!-- Strings: <input type="number" v-model="strings" /> -->
  <br />
  <br />
  <div class="fretboard">
    <div class="strings">
      <div
        class="string-wrap"
        v-for="(string, index) in [...Array(strings)]"
        :key="`string-${index}`"
      >
        <div class="string-fret" v-for="(fret, findex) in frets" :key="fret">
          <div class="string-fret-indicator">
            {{ notes[findex + notes.indexOf(tuning[index])] }}
          </div>
        </div>
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
const notes = [
  "C",
  "C#",
  "D",
  "D#",
  "E",
  "F",
  "F#",
  "G",
  "G#",
  "A",
  "A#",
  "B",
  "C",
  "C#",
  "D",
  "D#",
  "E",
  "F",
  "F#",
  "G",
  "G#",
  "A",
  "A#",
  "B",
  "C",
  "C#",
  "D",
  "D#",
  "E",
  "F",
  "F#",
  "G",
  "G#",
  "A",
  "A#",
  "B",
  "C",
  "C#",
  "D",
  "D#",
  "E",
  "F",
  "F#",
  "G",
  "G#",
  "A",
  "A#",
  "B",
];
const singleDotFrets = [3, 5, 7, 9, 15, 17, 19, 21];
const tuning = ["E", "A", "D", "G", "B", "E"];
export default {
  name: "App",
  components: {},
  data() {
    return {
      tuning: tuning.reverse(),
      notes,
      strings: 6,
      singleDotFrets,
      frets: 20,
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
}
.strings {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 100%;
}
.string-wrap {
  position: relative;
  width: 100%;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
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
.string-fret {
  position: relative;
  z-index: 5;
  border-radius: 15px;
  text-align: center;
  width: 90px;
}
.string-fret-indicator {
  font-family: sans-serif;
  font-weight: bold;
  display: inline-flex;
  background: white;
  border-radius: 15px;
  height: 15px;
  width: 15px;
  padding: 5px;
  border: 1px solid black;
  text-align: center;
  justify-content: center;
  align-items: center;
}

.frets {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
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
