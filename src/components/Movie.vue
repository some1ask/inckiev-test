<template>
  <div class="movies">
    <div class="movies__sort">
      <div class="movies__sort__item">
        <input type="radio" name="radio" id="sort1" @click="alphabetSort" />
        <label for="sort1"
          >отсортировать блоки по заголовку согласно алфавитного порядка</label
        >
      </div>
      <div class="movies__sort__item">
        <input
          type="radio"
          name="radio"
          id="sort2"
          value="leftSort"
          v-model="picked"
        />
        <label for="sort2"
          >вывести все блоки в формате “изображения - слева, текст -
          справа”</label
        >
      </div>
      <div class="movies__sort__item">
        <input
          type="radio"
          name="radio"
          id="sort3"
          value="chessSort"
          v-model="picked"
        />
        <label for="sort3"
          >вывести все блоки в формате “изображения - слева, текст - справа” и
          наоборот в шахматном порядке</label
        >
      </div>
    </div>
    <div v-for="(movie, index) in movies" :key="index" class="movies__wrapper">
      <div class="movies__info" :class="classObject">
        <h1>{{ movie.original_title }}</h1>
        <p>{{ movie.overview }}</p>
      </div>
      <div class="movies__poster">
        <img
          :src="`https://image.tmdb.org/t/p/w185_and_h278_bestv2${movie.poster_path}`"
          :alt="`${movie.original_title}`"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      picked: null,
      movies: [],
    };
  },
  mounted() {
    this.getMovies();
  },
  computed: {
    classObject: function () {
      return {
        "left-sorted": this.picked === "leftSort",
        "chess-sorted": this.picked === "chessSort",
      };
    },
  },
  watch: {
    picked: function () {
      console.log(this.picked);
    },
  },
  methods: {
    async getMovies() {
      const api =
        "https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1";
      try {
        await fetch(api)
          .then((response) => {
            return response.json();
          })
          .then((data) => {
            data.results.length = 5;
            this.movies = data.results;
          });
      } catch (error) {
        console.log(error);
      }
    },
    alphabetSort() {
      let sorted = this.movies.sort((a, b) => {
        if (a.original_title > b.original_title) {
          return 1;
        } else {
          return -1;
        }
      });
      this.movies = sorted;
    },
  },
};
</script>

<style lang="scss" scoped>
.movies {
  &__sort {
    width: 65%;
    margin: 20px auto;
    font-size: 14px;
    line-height: 30px;
    &__item {
      display: flex;
      align-items: center;
    }
  }
  &__wrapper {
    display: flex;
    height: 400px;
    width: 75%;
    margin: 0 auto;
    margin: 20px auto;
    padding: 20px;
    justify-content: space-around;
    align-items: center;
    background: #027d84;
    &:nth-of-type(even) {
      & .movies__info.chess-sorted {
        order: 1;
      }
      & .movies__info {
        order: 1;
      }
    }
    & .movies__info.left-sorted {
      order: 1;
    }
  }
  &__info {
    width: 60%;
    padding: 20px;
    h1 {
      margin: 10px 0 0 0;
    }
    p {
      font-size: 14px;
      line-height: 15px;
      text-align: justify;
    }
  }
}
</style>