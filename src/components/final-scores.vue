<template>
  <table class="final-scores" v-if="Object.keys(scores).length > 0">
    <thead>
    <tr>
      <th>Speler</th>
      <th>Score</th>
    </tr>
    </thead>

    <tbody>
    <tr v-for="(score, name) in scores" :key="score">
      <td>{{ name }}</td>
      <td> {{ calculateScore(score) }}</td>
    </tr>
    </tbody>
  </table>
</template>

<script setup lang="ts">
const props = defineProps(['scores']);

function calculateScore(score: Record<string, number>) {
  return Object.values(score).reduce((acc: number, val: number) => acc + val, 0);
}
</script>

<style>
table.final-scores {
margin-top: 10px;
}

table.final-scores th {
  border-radius: 5px 5px 0 0;
  background: rgba(0, 0, 0, 0.3);
  margin: 0;
  padding: 10px;
  text-align: left;
  color: rgba(255, 255, 255, 0.8);
}

table.final-scores td:first-child {
  width: 100%;
}

table.final-scores td:last-child {
  text-align: center;
  font-weight: bold;
}

table.final-scores tr {
  background: rgba(0, 0, 0, 0.2);
}

table.final-scores tr:last-child td:first-child {
  border-radius: 0 0 0 5px;
}

table.final-scores tr:last-child td:last-child {
  border-radius: 0 0 5px 0;
}

table.final-scores td {
  color: #fff;
  padding: 10px;
  font-weight: 300;
  text-transform: capitalize;
}

</style>
