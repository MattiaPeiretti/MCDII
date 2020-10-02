<template>
  <div>
    <navbar />
    <Nuxt />
    <span class="credits"
      >A website by
      <a href="https://mattiapeiretti.com/" target="_blank">Mattia Peiretti</a>.
      Opensouce
      <a href="https://github.com/MattiaPeiretti/MCDII" target="_blank"
        >Repo</a
      ></span
    >
  </div>
</template>

<style>
:root {
  --foregroundColor: #000;
  --primaryColor: #ff4d00;
  --secondaryColor: #275efe;
  --highlightColor: #ff763c;
  --normalShadowColor: rgba(0, 0, 0, 0.2);
  --highlightShadowColor: var(--normalShadowColor);



  --navbarForegroundColor: var(--foregroundColor);
  --navbarBackgroundColor: #fff;
  --navbarLinkHighlightColor: var(--primaryColor);
  --navbarMobileMenuBackgroundColor: var(--primaryColor);
  --navbarMobileMenuForegroundColor: #fff;

  --interfaceBorderRadius: 4px;
  --interfaceBackgroundColor: #fff;
  --interfaceActiveColor: var(--primaryColor);
  --interfaceActiveInnerColor: #fff;
  --interfaceHighlightColor: var(--highlightColor);
  --interfaceDisabledColor: #ccc;
  --interfaceDisabledInnerColor: #ddd;
  --interfaceForegroundColor: var(--foregroundColor);
  --interfaceFocusColor: var(--interfaceActiveColor);
  --interfaceHeaderBackgroundColor: #fff;
  --interfaceItemsBorderColor: #bbc1e1;
  --interfaceItemsBorderHoverColor: #aaa;
  --interfaceIdleBackgroundColor: #fff;
  --interfaceActiveBackgroundColor: var(--interfaceActiveColor);
  --interfaceSeparatorColor1: #eee;
  --interfacePrimaryButtonBackgroundColor: linear-gradient(
    180deg,
    rgba(255, 77, 0, 1) 70%,
    rgba(255, 100, 0, 1) 100%
  );
  --interfacePrimaryButtonForegroundColor: #fff;

  --consoleBackgroundColor: #f8f8f8;
  --consoleForegroundColor: var(--foregroundColor);
}

html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

.credits {
  position: fixed;
  bottom: 10px;
  right: 10px;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

h1,
h2,
h3,
h4 {
  font-family: "Montserrat", sans-serif;
}
</style>
