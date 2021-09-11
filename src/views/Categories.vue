<template>
  <div class="categories">
    <div class="flex-container">
      <p v-if="errorMsg">{{ errorMsg }}</p>
      <div class="flex-child">
        <h3>Category List</h3>
        <div class="categories" v-for="catName in categories" :key="catName.id">
          <p class="cat" @click="getJoke(catName)">{{ catName }}</p>
        </div>
      </div>
      <div class="flex-child">
        <h3>Joke list</h3>
        <div class="jokes" v-for="joke in jokes" :key="joke.id">
          <p>{{ joke.value }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'CategoryList',
  created () {
    this.getCategories()
  },
  data() {
    return {
      categories: [],
      jokes: [],
      errorMsg: '',
    }
  },
  
  methods: {
    getCategories() {
      axios
        .get('https://api.chucknorris.io/jokes/categories')
        .then((response) => {
          this.categories = response.data
          console.log(this.categories)
        })
        .catch((error) => {
          console.log(error)
          this.errorMsg = 'Error retrieving data'
        })      
    },

    getJoke(catName) {
      axios
        .get('https://api.chucknorris.io/jokes/random', {
          params: {
            category: catName
          }
        })
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

h3 {
  text-align: center;
  border: none;
  outline: none;
  background: none;
  width: 68%;
  max-width: 150px;
  background-color: #496583;
  padding: 16px;
  border-radius: 8px;
  color: #FFF;
  font-size: 14px;
  text-transform: uppercase;
  margin-bottom: 8px;
  transition: 0.4s;
}

.flex-container {
  display: flex;
}

.flex-child {
  flex: 1;
  border: 2px solid #496583;
  padding-left: 20px;
  width: 40%;
  max-width: 1500px;
}  

.flex-child:first-child {
  margin-right: 20px;
  width: 40%;
  max-width: 200px;
} 

p {
  padding: 16px;
  margin-right: 20px;
  background-color: #42B883;
  color: #FFF;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-size: 16px;
}

.cat {
  cursor: pointer;
  text-transform: uppercase;
}

</style>