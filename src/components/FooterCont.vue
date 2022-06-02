<template>
  <footer id="footer">
    <div>
      <h4>email</h4>
      <a href="mailto:lhw1847@gmail.com">lhw1847@gmail.com</a>
    </div>
    <div>
      <h4>Kakao</h4>
      <router-link to="#">LeeHyunwoo</router-link>
    </div>
    <div>
      <h4>soail</h4>
      <ul>
        <li><router-link to="#">Youtube</router-link></li>
        <li><router-link to="#">Instargram</router-link></li>
        <li><router-link to="#">Github</router-link></li>
        <li><router-link to="#">Cafe</router-link></li>
        <li><router-link to="#">Reference</router-link></li>
        <li><router-link to="#">Tutorials</router-link></li>
        <li><router-link to="#">CSS</router-link></li>
      </ul>
    </div>
  </footer>
</template>
<style lang="scss">
#footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  color: var(--black);
  border-top: 1px solid var(--light_border);
  background-color: var(--light_bg);
  display: flex;
  align-items: center;
  font-family: "Rajdhani";
  z-index: 1000;

  div {
    text-align: center;
    padding: 1.4rem;
  }
  h4,
  ul {
    display: inline-block;
  }

  h4 {
    font-weight: 500;
    padding: 0 0.6em;
    text-transform: capitalize;
  }
  a {
    position: relative;

    &::before {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0;

      width: 100%;
      height: 1px;
      background: var(--black);
      transform: scaleX(0);
      transition: all 0.3s ease;
    }
    &:hover::before {
      transform: scaleX(1);
    }
  }
  div:nth-child(1) {
    flex: 1 1 25%;
    border-right: 1px solid var(--light_border);
  }
  div:nth-child(2) {
    flex: 1 1 20%;
    border-right: 1px solid var(--light_border);
  }
  div:nth-child(3) {
    flex: 1 1 55%;

    li {
      display: inline;

      a {
        display: inline-block;
        padding: 0 0.6em;
        transition: all 0.3s;
        &::before {
          left: 0.6em;
          width: calc(100% - 1.2rem);
        }
      }
    }
  }
}

//미디어 커리
@media (max-width: 1060px) {
  #footer {
    div:nth-child(1) {
      h4 {
        display: none;
      }
    }
    div:nth-child(2) {
      display: none;
    }
    div:nth-child(3) {
      display: none;
    }
  }
}
</style>
