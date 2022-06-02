<template>
  <HeaderCont />
  <main id="main">
    <TitleCont name1="movie" name2="reference" />
    <section class="movie__cont">
      <div class="container">
        <div class="movie__inner">
          <div class="popular__list">
            <h2>인기영화</h2>
            <swiper
              :slidesPerView="5"
              :spaceBetween="30"
              :autoplay="{
                delay: 1000,
                disableOnInteraction: false,
              }"
              :pagination="{
                clickable: true,
              }"
              :modules="modules"
              class="mySwiper"
            >
              <swiper-slide
                class="swiper-slide"
                v-for="(movie, index) in popular"
                :key="movie.id"
              >
                <span class="num">{{ index + 1 }}</span>
                <img
                  :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
                  :alt="movie.title"
                />
              </swiper-slide>
            </swiper>
          </div>
          <div class="youtube__search">
            <form @submit.prevent="SearchMovies()">
              <div>
                <label for="search" class="sr-only">검색하기</label>
                <input
                  type="search"
                  id="search"
                  placeholder="검색하기"
                  v-model="search"
                />
                <button type="submit">검색</button>
              </div>
            </form>
          </div>
          <div class="movie__list">
            <ul>
              <li v-for="movie in movies" :key="movie.id">
                <a
                  target="_blank"
                  :href="`https://www.themoviedb.org/movie/${movie.id}?language=ko`"
                  ><img
                    :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
                    :alt="movie.title"
                /></a>
                <p class="title">{{ movie.title }}</p>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    <ContactCont />
  </main>
  <FooterCont />
</template>
<script>
import HeaderCont from "@/components/HeaderCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { ref } from "vue";
import "swiper/css";
import "swiper/css/pagination";
import { Pagination, Autoplay } from "swiper";

export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
    Swiper,
    SwiperSlide,
  },

  setup() {
    const movies = ref([]);
    const popular = ref([]);
    const search = ref("superman");
    const SearchMovies = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=17ff27aacedc9b2f2e883983ccb96462&query=${search.value}&language=ko`,
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => {
          movies.value = data.results;
          search.value = "";
        })
        .catch((error) => console.log("error", error));
      // console.log(movies);
    };
    SearchMovies();
    const TopMovies = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      fetch(
        "https://api.themoviedb.org/3/movie/popular?api_key=17ff27aacedc9b2f2e883983ccb96462&language=ko&Page=1",
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => {
          popular.value = data.results;
          search.value = "";
        })
        .catch((error) => console.log("error", error));
      console.log(popular);
    };
    TopMovies();

    return {
      movies,
      popular,
      SearchMovies,
      TopMovies,
      search,
      modules: [Pagination, Autoplay],
    };
  },
};
</script>
<style lang="scss">
.swiper-pagination-bullet {
  opacity: 0;
}
.movie__cont {
  background: var(--light_bg);
  form {
    width: 98%;
  }
}
.popular__list {
  margin-bottom: 5%;
  overflow: hidden;
  .mySwiper {
    border-radius: 10px;
    overflow-x: hidden;
    display: flex;
    width: 99%;
    .swiper-slide {
      height: 320px;
      img {
        width: 100%;
        height: 100%;
      }
    }
  }
}
.movie__list {
  ul {
    display: flex;
    flex-wrap: wrap;

    li:nth-child(1) {
      // display: none;
    }
    li {
      margin: 1%;
      flex: 1 1 23%;
      max-width: 23%;
      img {
        height: 90%;
      }
      p {
        color: var(--black);
        font-family: var(--sub_font);
        padding-top: 7px;
      }
    }
  }
}
.youtube__search {
  position: relative;
  display: flex;
  justify-content: center;

  input {
    border: 1px solid var(--light_border);
    width: 100%;
    background: var(--light_bg);
    border-radius: 50px;
    padding: 1rem 5rem 1rem 2rem;
    color: var(--black);
    font-family: var(--subKor_font);
    margin-bottom: 5%;
  }
  button {
    position: absolute;
    right: 70px;
    top: 8px;
    background: transparent;
    border: 0;
    color: var(--black);
    font-family: var(--subKor_font);
    background: var(--light_bg);
    width: 40px;
    height: 40px;
    border: 1px solid var(--btn_boder);
    border-radius: 50%;
    font-size: 12px;
    transition: opacity 0.3s ease;
    &:active {
      opacity: 0.7;
    }
  }
}
@media (max-width: 1200px) {
  .movie__list {
    ul {
      li {
        flex: 1 1 30%;
        max-width: 30%;
      }
    }
  }
}
@media (max-width: 1060px) {
  .movie__list {
    ul {
      li {
        flex: 1 1 45%;
        max-width: 45%;
      }
    }
  }
}
@media (max-width: 600px) {
  .movie__list {
    ul {
      li {
        flex: 1 1 98%;
        max-width: initial;
      }
    }
  }
}
</style>
