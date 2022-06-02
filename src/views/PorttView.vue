<template>
  <HeaderCont />
  <main id="main">
    <TitleCont name1="portfolio" name2="site" />
    <section class="port__cont">
      <div class="container">
        <div class="port__inner">
          <article class="port__item" v-for="port in ports" :key="port.id">
            <figure class="img">
              <a :href="port.link" target="_blank"
                ><img :src="port.image" :alt="port.title"
              /></a>
            </figure>
            <div class="text">
              <h3>{{ port.title }}</h3>
              <p>{{ port.category }}</p>
            </div>
          </article>
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
    const ports = ref([]);

    const Portfolios = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };
      fetch(
        "https://webstoryboy.github.io/dothome1/portfolio.json",
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => (ports.value = data.data.ports))
        .catch((error) => console.log("error", error));
    };

    setTimeout(() => {
      Portfolios();
    }, 2000);

    return {
      ports,
      Portfolios,
    };
  },
};
</script>
<style lang="scss">
//port__cont
.port__cont {
  padding-bottom: 20vh;
  background: var(--light_bg);
}
.port__inner {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}
.port__item {
  flex: 1 1 30%;
  margin: 1%;
  max-width: 30%;
  .text {
    padding: 1.4rem;
    background-color: var(--gray);
    h3 {
      color: var(--black);
      font-family: var(--main_font);
      font-size: 2.6rem;
      line-height: 1;
      padding-top: 0.2em;
      text-transform: uppercase;
    }
    p {
      color: var(--black);
      font-family: var(--sub_font);
      margin-top: 0.4em;
    }
  }
}

@media (max-width: 900px) {
  .port__inner {
    justify-content: space-between;

    .port__item {
      max-width: initial;
    }
  }
}

//animation
// .port__inner {
//     opacity: 0;
//     transform: translate(0, 100px);
// }
</style>
