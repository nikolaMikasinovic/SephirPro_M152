<template>
    <div class="container">
      <div class="content" v-for="(noten, fach) in Fächer" :key="fach">
        <div class="Fach">{{ fach }}</div>
        <br>
        <div class="note" v-for="(note, index) in noten.noten" :key="index">
          <div>
            {{ parseFloat(note).toFixed(2) }}
            <button @click="deleteNote(fach, index)">❌</button>
          </div><br>          
        </div>
        <br>
        <div class="notenAdd"><input type="number" min="0" max="6" @keyup.enter="addNote($event, fach)" /></div>
        <br>
        <br>
        <div class="NotenSchnitt">Ø: {{ parseFloat(calculateAverageGrade(fach)).toFixed(2) }}</div>
      </div>
    </div>
    <table>
      <tbody>
        <tr>
          <td>
            <label type="text">Neues Fach: </label>
            <input type="text" @keyup.enter="addSubject($event)"/>
          </td>
        </tr>
        <tr>
          <td>Gesamter Ø</td>
          <td>{{ parseFloat(roundHalf(calculateAverageGradeFromAllSubjects())).toFixed(2) }}</td>
        </tr>
      </tbody>
    </table>
</template>

<script setup>
import { ref } from "@vue/reactivity";

const Fächer = ref({
  GES: { noten: [4, 5.5] },
  M151: { noten: [2, 5, 4] },
  M152: { noten: [6, 6] },
  M153: { noten: [6] },
  M306: { noten: [6, 6] },
  NWS: { noten: [6, 6] },
  SPK: { noten: [4.5] },
  SPO: { noten: [5.1] },
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

function calculateAverageGradeFromAllSubjects() {
  let sum = 0;
  let count = 0;
  for (let fach in Fächer.value) {
    for (let note of Fächer.value[fach].noten) {
      sum += note;
      count++;
    }
  }
  return sum / count;
}

function addSubject(e) {
  Fächer.value[e.target.value] = { noten: [] };
}

function roundHalf(num) {
    return Math.round(num*2)/2;
}
</script>
<style>
.home {
  display: grid;
  min-height: 100vh;
  min-width: 100vw;
  margin: 0;
  justify-content: center;
}
ul#Fächer {
  width: 50%;
}
</style>