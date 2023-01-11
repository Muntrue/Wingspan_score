<style>
table.score-board td{
  font-weight: 400;
  font-size: 20px;
}
</style>

<template>
  <table class="score-board">
    <tbody>
    <tr>
      <td style="width: 100%;">Veren</td>
      <td><input type="number" style="width:80px" v-model="score.feather"/></td>
    </tr>
    <tr>
      <td style="width: 100%;">Bonus kaarten</td>
      <td><input type="number" style="width:80px" v-model="score.bonus"/></td>
    </tr>
    <tr>
      <td style="width: 100%;">Einde ronde doelen</td>
      <td><input type="number" style="width:80px" v-model="score.end_round"/></td>
    </tr>
    <tr>
      <td style="width: 100%;">Eieren</td>
      <td><input type="number" style="width:80px" v-model="score.egg"/></td>
    </tr>
    <tr>
      <td style="width: 100%;">Eten op kaarten</td>
      <td><input type="number" style="width:80px" v-model="score.food"/></td>
    </tr>
    <tr>
      <td style="width: 100%;">Kaarten onder kaarten</td>
      <td><input type="number" style="width:80px" v-model="score.card"/></td>
    </tr>
    <tr>
      <td style="width: 100%;">Nectar</td>
      <td><input type="number" style="width:80px" v-model="score.nectar"/></td>
    </tr>
    </tbody>
  </table>
</template>

<script setup lang="ts">
import {onMounted, ref, watch} from "vue";

const score = ref({
  feather: 0,
  bonus: 0,
  end_round: 0,
  egg: 0,
  food: 0,
  card: 0,
  nectar: 0
});

const emit = defineEmits(['update:modelValue']);
const props = defineProps(['modelValue']);

watch(score, async (newScore) => {
  emit('update:modelValue', newScore);
});

onMounted(() => {
  if (!Object.keys(props.modelValue).includes('feather')) {
    emit('update:modelValue', score.value);
  } else {
    score.value = props.modelValue
  }
});

</script>
