<template>
  <nav>
    <div class="nav-container">
      <a href="/" class="nav-logo">
        <img src="@/assets/Logo.png" alt="logo" />
        <h1>MCDII</h1>
      </a>
      <div class="nav-buttons">
        <ul class="links">
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

<script></script>

<style scoped lang="scss">
nav {
  box-shadow: 0 2px 5px -2px var(--normalShadowColor);
  position: fixed;
  z-index: 999;
  background-color: white;
  width: 100%;
  background-color: var(--navbarBackgroundColor);

  .nav-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 5px;
    width: 90%;
    margin-left: auto;
    margin-right: auto;
    height: 50px;

    .nav-buttons {
      ul {
        li {
          display: inline;
          margin-left: 20px;
          line-height: 20px;

          a {
            text-decoration: none;
            color: var(--navbarForegroundColor);
          }

          a,
          a > span {
            position: relative;
            color: inherit;
            text-decoration: none;
            line-height: 24px;
            &:before,
            &:after {
              content: "";
              position: absolute;
              transition: transform 0.5s ease;
            }
          }

          a {
            display: inline-block;
            padding-top: 10px;
            padding-bottom: 2px;
            overflow: hidden;
            &:before {
              left: 0;
              bottom: 0;
              width: 100%;
              height: 2px;
              background: var(--navbarLinkHighlightColor);
              transform: translateX(-100%);
            }
            &:hover:before {
              transform: translateX(0);
            }
          }
        }
      }
    }
    .nav-logo {
      display: flex;
      align-items: center;
      text-decoration: none !important;
      color: var(--navbarForegroundColor);

      img {
        max-width: 60px;
        padding: 5px;
      }

      h1 {
        margin-left: 10px;
      }
    }
  }
}
</style>
