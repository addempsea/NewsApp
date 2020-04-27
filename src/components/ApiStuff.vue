<template>
  <div class="container-fluid nw">
    <h1 class="py-3">Top Headlines from around the world</h1>
    <form class="container">
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <label class="input-group-text" for="inputGroupSelect01"
            >Country</label
          >
        </div>
        <select class="custom-select" id="inputGroupSelect01" v-model="country">
          <option value="us">USA</option>
          <option value="ng">Nigeria</option>
          <option value="de">Germany</option>
          <option value="jp">Japan</option>
          <option value="nz">New Zealand</option>
          <option value="gb">England</option>
          <option value="ca">Canada</option>
        </select>
      </div>

      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <label class="input-group-text" for="inputGroupSelect01"
            >Category</label
          >
        </div>
        <select
          class="custom-select"
          id="inputGroupSelect01"
          v-model="category"
        >
          <option value="general">General</option>
          <option value="health">Health</option>
          <option value="science">Science</option>
          <option value="sports">Sports</option>
          <option value="entertainment">Entertainment</option>
          <option value="technology">Tech</option>
          <option value="business">Business</option>
        </select>
      </div>
      <button type="button" class="btn btn-dark mb-3" @click="getNews">
        Get News
      </button>
    </form>

    <div class="container">
      <div class="main__hero" v-for="(item, index) in items" :key="index">
        <a :href="item.url" class="picture__link">
          <div>
            <img :src="item.urlToImage" :alt="item.title" class="images my-1" />
          </div>
        </a>
        <div class="content__body">
          <h2>
            <a :href="item.url">
              {{ item.title }}
            </a>
          </h2>
          <p>
            {{ item.description }}
          </p>
          <hr />
          <hr />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Api",
  data() {
    return {
      country: "",
      category: "",
      items: [],
    };
  },

  mounted() {
    (this.country = "ng"), (this.category = "health");
    this.getNews();
  },

  methods: {
    getNews() {
      var apiSource = "https://newsapi.org/v2/top-headlines?country=";
      var ctr = this.country;
      var linkup = "&category=";
      var cat = this.category;
      var apiKey = "&apiKey=360e9255e3ce425881637a308ecf0632";
      var source = apiSource + ctr + linkup + cat + apiKey;
      this.$http.get(source).then((response) => {
        this.items = response.data.articles;
      });
    },
  },
};
</script>
<style scoped>
.images {
  height: 100px;
  width: 150px;
}
a:hover {
  text-decoration: underline;
}
a {
  color: bisque;
}
.nw {
  background: rgb(161, 153, 147);
}
</style>
