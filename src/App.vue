<script setup>
import { ref, computed, onMounted } from 'vue';

const wins = ref(0);
const draws = ref(0);
const losses = ref(0);

const choise = ref(null);
const computerChoise = ref(null);
const verdict = ref(null);

const outcomes = {
  rock: {
    rock: 'draw',
    paper: 'loss',
    scissors: 'win',
  },
  paper: {
    rock: 'win',
    paper: 'draw',
    scissors: 'loss',
  },
  scissors: {
    rock: 'loss',
    paper: 'win',
    scissors: 'draw',
  },
};

const winPercentage = computed(() => {
  const total = wins.value + draws.value + losses.value;
  return total ? (wins.value / total) * 100 : 0;
});

const play = (c) => {
  const choices = ['rock', 'paper', 'scissors'];
  const random = Math.floor(Math.random() * choices.length);
  computerChoise.value = choices[random];

  const outcome = outcomes[c][computerChoise];

  if (outcome === 'win') {
    wins.value++;
    verdict.value = 'You win!';
  } else if (outcome === 'loss') {
    losses.value++;
    verdict.value = 'You loss!';
  } else {
    draws.value++;
    verdict.value = 'It is a draw!';
  }

  SaveGame();
};

const SaveGame = () => {
  localStorage.setItem('wins', wins.value);
  localStorage.setItem('draws', draws.value);
  localStorage.setItem('losses', losses.value);
};

const LoadGame = () => {
  wins.value = parseInt(localStorage.getItem('wins')) || 0;
  draws.value = parseInt(localStorage.getItem('draws')) || 0;
  losses.value = parseInt(localStorage.getItem('losses')) || 0;
};
</script>

<template>
  <h1>Hello</h1>
</template>
