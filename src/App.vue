<script setup>

import { ref, computed } from 'vue';

// Número a adivinar
const randomNumber = ref(parseInt(Math.random() * 100) + 1)

// Variable de estado nos determina si estamos jugando o no
const isPlaying = ref(false)

// variable para almacenar todos los números que el jugador va probando
const previousGuesses = ref([])


// Número que ha escrito el usuario en el <input>
const currentGuess = ref("")

// número de intentos
const attempts = ref(10)

const startGame = () => {
  console.log("Game Starts")
  isPlaying.value = true
}

const checkGuess = () => {
  previousGuesses.value.push(currentGuess.value)
  currentGuess.value = ""
  attempts.value-- 
}

const lastNumber = computed(() => {
  return previousGuesses.value[previousGuesses.value.length - 1]
})

</script>

<template>
  <main>
    <h2>Number guessing game</h2>

    <section v-if="isPlaying">
      <p>Try and guess a random number between 1 and 100.</p>
      <p>You have 10 attempts to guess the right number.</p>
      <div id="wrapper">
        <label for="guessField">Guess a number</label>
        <input v-model="currentGuess" type="number" id="guessField">
        <button @click="checkGuess" class="button-check">Check Guess</button>

        <div v-show="lastNumber" class="resultParas">
          <p>Previous Guesses: <span class="guesses"> {{ previousGuesses.join("-") }}</span></p>
          <p>Last number checked: {{ lastNumber }}</p>
          <p>Guesses Remaining: <span class="lastResult">{{ attempts }}</span></p>
          <p v-if="randomNumber > lastNumber" style="color: green">El número debe ser mayor</p>
          <p v-else style="color: red">El número debe ser menor</p>

        </div>
      </div>
    </section>
    <section v-else>
      <button @click="startGame">Start Game</button>
    </section>
  </main>
</template>

<style>
.button-check {
  background-color: rgb(128, 70, 128);
}
</style>
