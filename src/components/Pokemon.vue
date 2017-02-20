<template>
  <div>
    <h1>{{ msg }}</h1>
    <button class="btn btn-primary" v-on:click="getPokemons()">Get a Poekmons</button>
    <div v-for="poekmon in poekmons">
      {{ poekmon.name }} <button class="btn btn-primary" v-on:click="addPokemons(poekmon)">Add</button>
    </div>
    <div v-for="poekmon in myPokemons">
      {{ poekmon.name }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Pokemon',
  data () {
    return {
      msg: 'Polemons List',
      poekmons: [],
      myPokemons: [],
      maxPokemon: 6
    }
  },
  methods: {
    getPokemons () {
      this.$http.get('/api/v2/pokemon').then(response => {
        // success callback
        console.log(response)
        this.poekmons = response.body.results
      }, response => {
        // error callback
      })
    },
    addPokemons (pokemon) {
      if (this.myPokemons.length <= this.maxPokemon) {
        this.myPokemons.push(pokemon)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
