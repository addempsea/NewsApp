<template>
  <div class="container">
    <template v-if="!isLoading">
      <div class="container">
        <div class="form-group">
          <label for="query">
            <b>What are you looking for?</b>
          </label>
          <input v-model="query" class="form-control" placeholder="enter search" />
          <button class="btn" @click="filt">Search</button>
        </div>

        <div class="nivies">
          <form class="form-group" @submit.prevent="addMovie">
            <input type="text" placeholder="Name" class="form-control" v-model="Name" />
            <select name="type" id class="form-control" v-model="Type">
              <option value="Movie">Music</option>
              <option value="Music">Movie</option>
            </select>
            <input type="text" placeholder="Url" class="form-control" v-model="Url" />
            <button>Add movie</button>
          </form>
        </div>

        <ul class="list-group">
          <!-- <li class="list-group-item" v-for="(item, index) in filtered" :key="index">
            <h3>{{item.Name}}</h3>
            <img :src="item.Url" :alt="item.Name+item.Type" />
            <button @click="deleted(index)">X</button>
          </li> -->
          <li class="list-group-item" v-for="(item, index) in movieList" :key="index">
            <h3>{{item.Name}}</h3>
            <img :src="item.Url" :alt="item.Name+item.Type" />
            <button @click="deleted(index)">X</button>
          </li>
        </ul>
      </div>
    </template>
    <div v-else>
      <h1>Loading.....</h1>
    </div>
  </div>
</template>

<script>
// import { setTimeout } from "timers";
export default {
  name: "Filter",

  data() {
    return {
      query: "",
      isLoading: true,
      Name: "",
      Url: "",
      Type: "",
      movieList: [],
      filtered: []
    };
  },

  methods: {
    filt() {
      let userInput = this.query;
      let result = this.movieList.filter(function(item) {
        return item.Name.includes(userInput);
      });

      this.filtered = result;
    },

    deleted(index) {
      return this.filtered.splice(index, 1);
    },

    addMovie() {
      let Data = {
        Name: this.Name,
        Type: this.Type,
        Url: this.Url
      };

      this.$http.post("http://localhost:3000/movies", Data);
      this.Name = '',
      this.Type = '',
      this.Url = ''
    }
  },

  mounted() {
    this.$http.get("http://localhost:3000/movies").then(response => {
      this.isLoading = false;
      this.movieList = response.data;
    });
  }
};
</script>