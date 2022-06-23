<template>
  <div class="container">
    <div class="content" v-for="(noten, fach) in Fächer" :key="fach">
      <div class="Fach">{{ fach }} <a>Ø: {{ parseFloat(calculateAverageGrade(fach)).toFixed(2) }}</a></div>
      <br>
      <div class="note" v-for="(note, index) in noten.noten" :key="index">
        <div>
          {{ parseFloat(note).toFixed(2) }}
          <button @click="deleteNote(fach, index)">❌</button>
        </div>
        <br>          
      </div>
      <br>
      <div class="notenAdd"><input type="number" min="0" max="6" @keyup.enter="addNote($event, fach)" /></div>
      <br>
      <br>
    </div>
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";

const Fächer = ref({
  GES: { noten: [4.5, 6] },
  M151: { noten: [3, 3, 4] },
  M152: { noten: [3, 6] },
  M153: { noten: [4] },
  M306: { noten: [6, 4] },
  NWS: { noten: [4, 6] },
  SPK: { noten: [4.5] },
  SPO: { noten: [3.2] },
  WUR: { noten: [5.3] },
});

function deleteNote(fach, note) {
  Fächer.value[fach].noten.splice(note, 1);
}

function addNote(e, fach) {
  let newNote = Math.min(6, Math.max(1, parseInt(e.target.value)));
  Fächer.value[fach].noten.push(newNote);
}

function calculateAverageGrade(fach) {
  let sum = 0;
  for (let note of Fächer.value[fach].noten) {
    sum += note;
  }
  return sum / Fächer.value[fach].noten.length;
}
</script>
