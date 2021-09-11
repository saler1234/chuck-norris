<template>
  <div class="home">
    <button class="get-more" @click="getJoke">Get more</button>
    <div class="joke-list">
      <p v-if="errorMsg">{{ errorMsg }}</p>
      <div class="jokes" v-for="joke in jokes" :key="joke.id">
        <p>{{ joke.value }}</p>
      </div>
      <p class="jokes">{{ this.startingJoke.value }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'JokeList',
  created () {
    this.getStartingJoke()
  },
  data() {
    return {
      startingJoke: [],
      jokes: [],
      errorMsg: '',
    }
  },
  
  methods: {
    getStartingJoke() {
      axios
        .get('https://api.chucknorris.io/jokes/random')
        .then((response) => {
          console.log(response.data)
          this.startingJoke = response.data
        })
        .catch((error) => {
          console.log(error)
          this.errorMsg = 'Error retrieving data'
        })      
    },

    getJoke() {
      axios
        .get('https://api.chucknorris.io/jokes/random')
        .then((response) => {
          this.jokes.unshift(response.data)
        })
        .catch((error) => {
          console.log(error)
          this.errorMsg = 'Error retrieving data'
        })
    }
  }
}
</script>

<style lang="scss">
.home {

  .get-more {
    border: none;
    outline: none;
    background: none;
    width: 100%;
    max-width: 150px;
    background-color: #496583;
    padding: 16px;
    border-radius: 8px;
    color: #FFF;
    font-size: 16px;
    text-transform: uppercase;
    margin-bottom: 8px;
    transition: 0.4s;
    &:active {
      background-color: #3B8070;
    }
  }
  
  .joke-list {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .jokes {
      margin: 8px;
      background-color: #42B883;
      color: #FFF;
      border-radius: 8px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      font-size: 16px;
      padding: 16px;
      max-width: 400px;
    }
  }
}
</style>