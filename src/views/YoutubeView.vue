<template>
  <HeaderCont />
  <main id="main">
    <TitleCont name1="youtube" name2="reference" />
    <section class="youtube__cont">
      <div class="container">
        <div
          class="youtube__inner"
          style="opacity: 1; transform: translate(0px, 0px)"
        >
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
          <div class="container">
            <div class="youtube__list">
              <ul>
                <li v-for="movie in movies" :key="movie.id.videoId">
                  <a
                    target="_blank"
                    :href="`https://www.youtube.com/watch?v=${movie.id.videoId}`"
                    ><img
                      :src="movie.snippet.thumbnails.medium.url"
                      :alt="movie.snippet.title"
                    />
                    <p>
                      {{ movie.snippet.title }}
                    </p></a
                  >
                </li>
              </ul>
            </div>
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
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
  },

  setup() {
    const movies = ref("");
    const search = ref("");
    const SearchMovies = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };

      fetch(
        "https://youtube.googleapis.com/youtube/v3/search?part=snippet&type=video&maxResults=30&q=숏박스&key=AIzaSyBFmDKyMThldJWBpgNzHFEqMZjTkpQdGyg",
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => (movies.value = data.items))
        .catch((error) => console.log("error", error));
      console.log(movies);
    };
    SearchMovies();
    return {
      movies,
      SearchMovies,
      search,
    };
  },
};
</script>
<style lang="scss">
.youtube__cont {
  background: var(--light_bg);
  form {
    width: 94%;
  }
}
.youtube__list {
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
        border-radius: 5px;
      }
      p {
        color: var(--black);
        font-family: var(--sub_font);
        padding-top: 7px;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
      }
    }
  }
}
</style>
