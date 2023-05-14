<template>
  <main>
    <h2>Parookaville 2023 - Sonntag 23.7. - Timetable (TBA)</h2>
    <h2 class="info">Zeiten noch nicht bekannt</h2>
    <table role="grid" ref="tableEl" :style="{'--font-size': fontSize+'px'}">
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col" v-for="h in headers">{{ h }}</th>
        </tr>
      </thead>
      <tbody>
        <Row v-for="row in table" :data="row"></Row>
      </tbody>
    </table>
  </main>
  <button class="zoom" @click="fontSize++">+</button>
  <button class="zoom" @click="fontSize--">-</button>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import Row from '../components/Row.vue';

/* ---------------- props ------------------- */
/* ---------------- data -------------------- */
const tableByStages = [
  [],
  [
    "Afrojack",
    "Kygo",
    "Oliver Heldens",
    "Timmy Trumpet",
    "Alle Farben",
    "Fedde Le Grand",
    "Mattn",
    "Neelix",
    "Showtek",
  ],
  [
    "Scooter",
    "Finch",
    "Harris & Ford",
    "HBz",
    "Jan-Christian Zeller",
    "Kasalla",
  ],
  [
    "Andrew Rayel",
    "Ben Gold",
    "Benjamin R",
    "Cosmic Gate",
    "Estiva",
    "Gareth Emery",
    "Giuseppe Ottaviani",
    "Paul Van Dyk",
    "Scott Project",
  ],
  [
    "Atmozfears",
    "Hard Driver",
    "Jebroer",
    "LNY TNZ",
    "Lost Identitiy",
    "Noel Holler",
    "Rooler",
    "Teknoclash",
    "Tiefblau",
    "Timbo & This Chris",
  ],
  [
    "Brandon",
    "Curbi",
    "Die Gebrüder Brett",
    "Gestört Aber Geil",
    "Jerome",
    "Juicy M",
    "Moksi",
    "Neptunica",
    "Oliver Magenta",
    "Vize",
  ],
  [
    "Rainer Zonneveld",
    "Christopher Bongard",
    "Claptone",
    "Popof",
    "Sarazar",
    "Space 92",
    "Stella Bossi",
    "Township Rebellion",
  ],
  [
    "",
  ]
]
fillTime(15, 30, 22)

/* ---------------- refs -------------------- */
const tableEl = ref(null);
const fontSize = ref(16);
const headers = ref([
  "Mainstage (EDM)", "Bills Factory", "Cloud Factory (Trance)", "Power Plant (Hardstyle)", "Time Lab (Funky Techno)", "Dessert Valley (Chillout Techno)", "Brainwash",
])

/* ---------------- computed ---------------- */
/* ---------------- functions --------------- */
/* ---------------- watchers ---------------- */
/* ------------- lifecycle hooks ------------ */

const table = computed(() => {
  const rows = tableByStages.length;
  const cols = tableByStages[0].length;
  const transposed = [];
  
  for (let j = 0; j < cols; j++) {
    transposed[j] = [];
    for (let i = 0; i < rows; i++) {
      transposed[j][i] = tableByStages[i][j];
    }
  }
  
  return transposed;
})


function fillTime(startHour, intervalMinutes, intervals) {
  let currentDate = new Date();
  currentDate.setHours(startHour, 0, 0, 0);

  for (let i = 0; i < intervals; i++) {
    const hour = String(currentDate.getHours()).padStart(2, '0');
    const minute = String(currentDate.getMinutes()).padStart(2, '0');
    const timeString = `${hour}:${minute}`;
    
    tableByStages[0].push(timeString);
    
    currentDate.setMinutes(currentDate.getMinutes() + intervalMinutes);    
  }
}

</script>

<style>
/* sticky row and column based on https://codepen.io/jon/pen/JZNvap */
body {
  display:flex;
  height:100vh;
  justify-content: center;
}

#app {
  overflow:scroll;
}

thead tr > th {
  background-color: var(--background-color);
  position: sticky;
  z-index:2;
  top: 0;
}

thead tr > :first-child {
  z-index:3;
  left:0;
  top:0;
}

tbody tr > :first-child {
  background-color: var(--background-color);
  position: sticky;
  z-index:1;
  left:0;
}

/* custom style */
.zoom {
  float: right;
  position: fixed;
  border-radius: 2em;
  width: 3em;
  padding: 0;
  right: 5%;
  bottom: 2.5em;
  z-index: 4;
}

.zoom:last-of-type{
  bottom: 0;
}

main {
  padding-bottom: 10em;
}

h2 {
  background-color: var(--secondary);
  border-radius: 0.2em;
  padding: 0.2em;
}

.info {
  background-color: var(--del-color);
}

th {
  font-weight: bolder;
}
th, td {
  padding: 0.5em;
}
</style>
