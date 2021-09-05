<template>
  <div class="home">
    <button @click="getJoke">Učitaj još</button>
    <p v-if="errorMsg">{{ errorMsg }}</p>
    <!-- <div v-for="joke in jokes" :key="joke.id"> -->
      <p>{{ this.jokes.value }}</p>
    <!-- </div> -->
    <p>{{ this.startingJoke.value }}</p>
  </div>
</template>

<script>
// import { ref, reactive, onMounted } from 'vue';
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
          console.log(response.data)
          if(this.jokes.length == 0) {
            this.jokes = response.data
          } else {
            console.log(this.jokes.value)
          }
        })
        .catch((error) => {
          console.log(error)
          this.errorMsg = 'Error retrieving data'
        })
    }
  }
  // setup() {
    
  //   }
    // const jokeList = ref([]);
    // const randomJoke = () => {
    //   fetch(`https://api.chucknorris.io/jokes/random`)
    //     .then(response => response.json())
    //     .then(data => {
    //       jokeList.value = data.result;
    //     });
    //     console.log(jokeList);
    // };

    // return {
    //   jokeList,
    //   randomJoke
    // }
  // }
}
</script>
