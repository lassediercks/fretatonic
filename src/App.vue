<template>
  <!-- Strings: <input type="number" v-model="strings" /> -->
  {{ newTuning }}
  key:
  <select v-model="selectedKey">
    <option :value="keyNote" v-for="keyNote in notes" :key="keyNote">
      {{ keyNote }}
    </option>
  </select>
  <br />
  <br />
  scale:
  <select v-model="scale">
    <option
      :value="scaleName"
      v-for="(scaleSelect, scaleName) in scalesIndexes"
      :key="scaleSelect"
    >
      {{ scaleName }}
    </option>
  </select>
  <br />
  <br />
  <!-- {{ Object.entries(scales) }} -->

  <div class="fretboard">
    <div class="strings">
      <div
        class="string-wrap"
        v-for="(s, string) in [...Array(strings)]"
        :key="`string-${string}`"
      >
        <div
          class="string-fret"
          v-for="(f, fretposition) in frets"
          :key="fretposition"
        >
          <Indicator
            :note="getNote(fretposition, string)"
            :inScale="currentScale.includes(getNote(fretposition, string))"
          />
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

  <br />
  <br />
  tuning:
  <div>
    <select v-model="firststringtune">
      <option :value="tuneNote" v-for="tuneNote in notes" :key="tuneNote">
        {{ tuneNote }}
      </option>
    </select>
    <select v-model="secondstringtune">
      <option :value="tuneNote" v-for="tuneNote in notes" :key="tuneNote">
        {{ tuneNote }}
      </option></select
    ><select v-model="thirdstringtune">
      <option :value="tuneNote" v-for="tuneNote in notes" :key="tuneNote">
        {{ tuneNote }}
      </option></select
    ><select v-model="forthstringtune">
      <option :value="tuneNote" v-for="tuneNote in notes" :key="tuneNote">
        {{ tuneNote }}
      </option></select
    ><select v-model="fifthstringtune">
      <option :value="tuneNote" v-for="tuneNote in notes" :key="tuneNote">
        {{ tuneNote }}
      </option></select
    ><select v-model="sixthstringtune">
      <option :value="tuneNote" v-for="tuneNote in notes" :key="tuneNote">
        {{ tuneNote }}
      </option>
    </select>
  </div>
</template>

<script>
const singleDotFrets = [3, 5, 7, 9, 15, 17, 19, 21];

import Indicator from "./components/indicator.vue";
import { notes, scalesIndexes } from "./util";

export default {
  name: "App",
  components: { Indicator },
  data() {
    return {
      firststringtune: "E",
      secondstringtune: "A",
      thirdstringtune: "D",
      forthstringtune: "G",
      fifthstringtune: "B",
      sixthstringtune: "E",
      test: "minor",
      scale: "major",
      selectedKey: "E",
      fretboardnotes: new Array(5).fill(notes).flat(),
      notes,
      strings: 6,
      singleDotFrets,
      frets: 20,
      scalesIndexes,
    };
  },
  computed: {
    tuning() {
      return [
        this.firststringtune,
        this.secondstringtune,
        this.thirdstringtune,
        this.forthstringtune,
        this.fifthstringtune,
        this.sixthstringtune,
      ].reverse();
    },

    currentScale() {
      let notesInKey = Array.from(notes);
      notesInKey = notesInKey.concat(
        notesInKey.splice(0, notes.indexOf(this.selectedKey))
      );
      let result = [];
      notesInKey.forEach((note) => {
        let index = notesInKey.indexOf(note);
        if (scalesIndexes[this.scale].includes(index)) {
          result.push(note);
        }
      });
      return result;
    },
  },
  methods: {
    getNote(fretposition, string) {
      return this.fretboardnotes[
        fretposition + notes.indexOf(this.tuning[string])
      ];
    },
    // thePenatoniker(){

    // }
  },
};
</script>

<style>
:root {
  --fret-width: 70px;
}

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
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  z-index: 5;
  height: 50px;
  border-radius: 15px;
  text-align: center;
  width: var(--fret-width);
}
.string-fret:first-child .string-fret-indicator {
  transform: translateX(-30px);
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
  width: var(--fret-width);
  border-right: 1px solid black;
}
.fret:first-child {
  border-right-width: 3px;
}
.dots {
  position: absolute;
  top: 100%;
  display: flex;
  justify-content: center;
  width: 100%;
}
</style>
