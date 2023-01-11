<template>
  <main id="app">
    <div class="container">
      <form onsubmit="return false" v-if="players.length < 4">
        <input type="text" placeholder="Voeg speler toe" ref="playerInput"/>
        <button @click="addPlayer" class="addButton">Toevoegen</button>
      </form>

      <final-scores :scores="playerScores"/>

      <TabGroup v-if="players.length > 0">
        <TabList class="tablist">
          <Tab class="tab"
               v-for="player in players"
               :key="player"
               v-slot="{ selected }"
          ><span :class="{selected: selected}">{{ player }}</span>
          </Tab>
        </TabList>
        <TabPanels>
          <TabPanel v-for="player in players" :key="player">
            <div class="card">
              <h2>Scores</h2>
              <score-board v-model="playerScores[player]"/>
            </div>
          </TabPanel>
        </TabPanels>
      </TabGroup>

      <span v-else><br />Begin met spelers toevoegen</span>
    </div>
  </main>
</template>

<script setup lang="ts">
import {TabGroup, TabList, Tab, TabPanels, TabPanel} from '@headlessui/vue'
import {reactive, ref} from "vue";
import ScoreBoard from "@/components/score-board.vue";
import FinalScores from "@/components/final-scores.vue";

const players = ref<Array<string>>([]);
const playerInput = ref<HTMLInputElement | null>(null);
const playerScores = reactive({}) as Record<string, object>;

function addPlayer() {
  if (playerInput.value && players.value.length < 4) {
    players.value.push(playerInput.value.value);

    playerScores[playerInput.value.value] = {};

    playerInput.value.value = "";
    playerInput.value.focus();
  }
}
</script>
