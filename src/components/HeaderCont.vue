<template>
  <header id="header">
    <div className="header__port">
      <router-link to="/port">portfoilo</router-link>
    </div>
    <div className="header__logo">
      <router-link to="/">LeeHyunwoo</router-link>
    </div>
    <div className="header__menu">
      <ul>
        <li><router-link to="/about">About</router-link></li>
        <li><router-link to="/refer">Reference</router-link></li>
        <li><router-link to="/youtube">Youtube</router-link></li>
        <li><router-link to="/movie">Movie</router-link></li>
        <li><router-link to="/contact">contact</router-link></li>
      </ul>
    </div>
  </header>
</template>
<style lang="scss">
#header {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  color: var(--black);
  border-bottom: 1px solid var(--light_border);
  background-color: var(--light_bg);
  padding: 0 1em;
  display: flex;
  align-items: center;
  font-family: "Rajdhani";
  z-index: 1000;

  .header__port,
  .header__menu {
    a {
      position: relative;

      &::before {
        content: "";
        position: absolute;
        left: 1rem;
        bottom: 1rem;
        width: calc(100% - 2rem);
        height: 1px;
        background: var(--black);
        transform: scaleX(0);
        transition: all 0.3s ease;
      }
      &:hover::before {
        transform: scaleX(1);
      }
    }
  }
}
.header__port {
  flex: 1 1 40%;
  a {
    display: inline-block;
    padding: 1rem;
    text-transform: capitalize;
  }
}
.header__logo {
  flex: 1 1 20%;
  text-align: center;
  a {
    display: inline-block;
    font-size: 1.6rem;
    padding: 1rem;
  }
}
.header__menu {
  flex: 1 1 40%;
  text-align: right;

  li {
    display: inline;

    a {
      display: inline-block;
      padding: 1rem;
    }
  }
}

//미디어 커리
@media (max-width: 1060px) {
  .header__port {
    display: none;
  }
  .header__menu {
    display: none;
  }
}
</style>
