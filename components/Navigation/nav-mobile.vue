<template>
  <nav>
    <div class="nav-container">
      <a href="/" class="nav-logo">
        <img src="@/assets/Logo.png" alt="logo" />
        <h1>MCDII</h1>
      </a>

      <div
        class="nav-burger"
        @click="isMenuOpened = !isMenuOpened"
        v-bind:class="{ 'nav-burger-open': isMenuOpened === true }"
      >
        <span></span>
        <span></span>
        <span></span>
      </div>

      <div class="nav-buttons">
        <ul class="links" v-bind:class="{ 'nav-open': isMenuOpened === true }">
          <li><a href="/console">Console</a></li>
          <li><a href="/about">About</a></li>
          <li>
            <a href="http://www-mars.lmd.jussieu.fr/mcd_python/" target="_blank"
              >Legacy Interface</a
            >
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data: () => {
    return {
      isMenuOpened: false
    };
  }
};
</script>

<style scoped lang="scss">
nav {
  box-shadow: 0 2px 5px -2px var(--normalShadowColor);
  width: 100%;
  height: 80px;
  position: absolute;
  z-index: 999;
  background-color: var(--navbarBackgroundColor);

  .nav-container {
    display: flex;
    align-items: center;
    width: 100%;
    height: 80px;

    .nav-buttons {
      ul {
        height: 100vh;
        width: 100%;
        position: absolute;
        top: 0;
        left: 0;
        background-color: var(--navbarMobileMenuBackgroundColor);
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        list-style-type: none;
        padding: 0 !important;
        z-index: 1;

        clip-path: circle(0 at 101% -01%);
        transition: clip-path 0.7s;

        li {
          padding: 5vw;

          a {
            text-decoration: none;
            color: var(--navbarMobileMenuForegroundColor);
            font-size: 9vw;
            font-family: "Montserrat", sans-serif;
          }
        }

        &.nav-open {
          clip-path: circle(1000px at 90% -10%);
          transition: clip-path 0.5s;
        }
      }
    }

    .nav-logo {
      display: flex;
      align-items: center;
      justify-content: space-between;
      text-decoration: none !important;
      color: var(--navbarForegroundColor);

      img {
        max-width: 80px;
        padding: 5px;
      }

      h1 {
        margin-left: 10px;
      }
    }

    .nav-burger {
      position: absolute;
      top: 0;
      right: 0;
      z-index: 999;
      width: 43px;
      height: 45px;
      margin: 20px;
      -webkit-transform: rotate(0deg);
      -moz-transform: rotate(0deg);
      -o-transform: rotate(0deg);
      transform: rotate(0deg);
      -webkit-transition: 0.7s ease-in-out;
      -moz-transition: 0.7s ease-in-out;
      -o-transition: 0.7s ease-in-out;
      transition: 0.7s ease-in-out;
      cursor: pointer;

      span {
        display: block;
        position: absolute;
        height: 5px;
        width: 100%;
        background: black;
        border-radius: 100px;
        opacity: 1;
        left: 0;
        -webkit-transform: rotate(0deg);
        -moz-transform: rotate(0deg);
        -o-transform: rotate(0deg);
        transform: rotate(0deg);
        -webkit-transition: 0.25s ease-in-out;
        -moz-transition: 0.25s ease-in-out;
        -o-transition: 0.25s ease-in-out;
        transition: 0.25s ease-in-out;

        &:nth-child(1) {
          top: 0px;
          -webkit-transform-origin: left center;
          -moz-transform-origin: left center;
          -o-transform-origin: left center;
          transform-origin: left center;
        }

        &:nth-child(2) {
          top: 12px;
          -webkit-transform-origin: left center;
          -moz-transform-origin: left center;
          -o-transform-origin: left center;
          transform-origin: left center;
        }

        &:nth-child(3) {
          top: 24px;
          -webkit-transform-origin: left center;
          -moz-transform-origin: left center;
          -o-transform-origin: left center;
          transform-origin: left center;
        }
      }

      &.nav-burger-open {
        span {
          background-color: var(--navbarBackgroundColor);

          &:nth-child(1) {
            -webkit-transform: rotate(45deg);
            -moz-transform: rotate(45deg);
            -o-transform: rotate(45deg);
            transform: rotate(45deg);
            top: -3px;
            left: 8px;
          }

          &:nth-child(2) {
            opacity: 0;
          }

          &:nth-child(3) {
            -webkit-transform: rotate(-45deg);
            -moz-transform: rotate(-45deg);
            -o-transform: rotate(-45deg);
            transform: rotate(-45deg);
            top: 27px;
            left: 8px;
          }
        }
      }
    }
  }
}
</style>
