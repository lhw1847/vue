<template>
  <HeaderCont />
  <main id="main">
    <TitleCont name1="reference" name2="book" />
    <section class="refer__cont">
      <div class="container">
        <div
          class="refer__inner"
          style="opacity: 1; transform: translate(0px, 0px)"
        >
          <h2>CSS</h2>
          <ul class="refer__list">
            <li v-for="htmlRefer in items" :key="htmlRefer.id">
              <a :href="htmlRefer.link" target="_blank"
                ><span class="id">{{ htmlRefer.id }}</span
                ><span class="title">{{ htmlRefer.title }}</span
                ><span class="desc">{{ htmlRefer.desc }}</span
                ><span class="use">{{ htmlRefer.use }}</span></a
              >
            </li>
          </ul>
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
    const items = ref([]);

    const Reference = () => {
      var requestOptions = {
        method: "GET",
        redirect: "follow",
      };
      fetch(
        "https://webstoryboy.github.io/dothome1/reference.json",
        requestOptions
      )
        .then((response) => response.json())
        .then((data) => (items.value = data.data.refer))
        .catch((error) => console.log("error", error));
    };
    Reference();
    return {
      items,
      Reference,
    };
  },
};
</script>
<style lang="scss">
.refer__cont {
  background-color: var(--light_bg);
  min-height: 100vh;
}
.refer__inner {
  h2 {
    color: var(--black);
    font-size: 2rem;
    margin-bottom: 1rem;
  }
  .img_table {
    display: flex;
    margin-bottom: 20px;

    .img {
      overflow: hidden;
      width: 40%;
      margin-right: 20px;
      margin-top: 20px;
      border: 2px solid var(--light_border);
      img {
        height: 100%;
      }
    }
    .table {
      margin-top: 20px;
    }
  }
}
.refer__list {
  border-top: 2px solid var(--light_border);
  border-bottom: 1px solid var(--light_border);
  a {
    display: block;
    color: var(--black);
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--light_border);
    padding: 1.3rem 0;
    transition: all 0.3s;
    font-family: var(--subKor_font);
    &:hover {
      background: var(--gray);
      color: var(--white);
    }
    span {
      display: inline-block;
    }
    span:nth-child(1) {
      width: 6%;
      text-align: center;
    }
    span:nth-child(2) {
      width: 20%;
    }
    span:nth-child(3) {
      width: 64%;
    }
    span:nth-child(4) {
      width: 10%;
      text-align: center;
    }
  }
}
.refer__table {
  margin-top: 200px;
  color: var(--black);
  font-family: var(--subKor_font);

  h3 {
    font-size: 3rem;
  }
  p {
    background-color: var(--light_bg);
    color: var(--black);
    padding: 1.4em;
  }
  .table {
    color: var(--black);
    font-family: var(--subKor_font);
    border: 1px solid var(--light_border);
    margin-top: 0.5em;

    th,
    td {
      font-weight: normal;
      padding: 1em;
      border-bottom: 1px solid var(--light_border);
      border-left: 1px solid var(--light_border);
    }

    thead {
    }
    tbody {
    }
  }
}
.refer__table:nth-child(2) {
  margin-bottom: 200px;
  margin-top: 0;
}
.refer__cont.light {
  background-color: var(--light_bg);
  .refer__inner {
    h2 {
      color: var(--black);
    }
    table {
      border-color: var(--black);
      color: var(--black);
      td {
        border-color: var(--black);
      }
    }
  }
}
//애니메이션
// .refer__inner {
//     opacity: 0;
//     transform: translateY(50px);
// }

// @media (max-width: 1250px){
//     .img_table {
//         flex-direction: column;

//         .img {
//             width: 100% !important;
//             max-height: 500px;
//             display: flex;
//             align-items: center;
//             img {
//             }
//         }
//     }
// }
</style>
