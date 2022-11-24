<template>
  <router-view />
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Bungee&family=PT+Sans&display=swap");
*,
*::after,
*::before {
  box-sizing: border-box;
}
:root {
  --color-accent-pink: #ef476f;
  --color-bg: #f5f5f5;
  --color-bg-input: #ffffff;
  --color-accent-yellow: #f5ab00;
  --color-accent-green: #06d6a0;
  --color-accent-blue: #118ab2;
  --color-font: #073b4c;

  font-family: "PT Sans", sans-serif;
  color: var(--color-font);
  font-size: 18px;
  max-width: 800px;
  margin: auto;
  background-color: var(--color-bg);
}
h1 {
  font-family: "Bungee", cursive;
}

.visually-hidden {
  border: 0;
  clip: rect(0 0 0 0);
  height: auto;
  margin: 0;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
  white-space: nowrap;
}
</style>
