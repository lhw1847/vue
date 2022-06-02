<template>
  <section class="cont__title">
    <div class="container">
      <h1>
        <strong>{{ name1 }}</strong>
        <em>{{ name2 }}</em>
      </h1>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    name1: String,
    name2: String,
  },
};
</script>
<style lang="scss">
//cont__title
.cont__title {
  padding: 10vmax 0;
  font-size: 5vmax;
  font-family: var(--main_font);
  text-transform: uppercase;
  line-height: 0.85;
  background: var(--light_bg);
  color: var(--black);

  em {
    display: block;
  }
}
@media (max-width: 600px) {
  .cont__title {
    text-align: center;
    padding-bottom: 10vw;
  }
}
</style>
