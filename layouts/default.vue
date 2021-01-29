<template>
  <main>
    <Nuxt />
  </main>
</template>

<script>
export default {
  head: {
    title: "Todo Trackster",
    meta: [
      {
        hid: 'description',
        name: 'description',
        content: 'Todo Trackster - Todo app created by Digvijaysinh Padhiyar.'
      },
      {
        hid: 'auther',
        name: 'auther',
        content: 'Digvijaysinh Padhiyar'
      },
      {
        hid: 'keywords',
        name: 'keyword',
        content: 'Digvijaysinh Padhiyar, Digvijay, Todo App, todo pwa, pwa, todo trackster'
      }
    ]
  }
}
</script>

<style>
/* VARIABLES */
:root {
  /* COLORS */
  --yellow: #f1c40f;
  --dark: #353b48;
  --white: #f5f6fa;
  --red: #c0392b;
  --green: #2ecc71;

  /* FONTS FAMILIES */
  --sketch: 'Cabin Sketch', cursive;
  --nunito: 'Nunito', sans-serif;
  --magic: 'Yusei Magic', sans-serif;
}

/* CSS RESET */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  overflow-x: hidden;
}

body {
  background-color: var(--yellow);
  color: var(--white);
  font-family: var(--nunito);
}

/* PREDEFINED CLASSES */
.container {
  margin: 0 auto;
  max-width: 1280px;
  width: 70%;
}

.textCenter {
  text-align: center;
}

.btn {
  display: inline;
  width: max-content;
  padding: 4px 6px;
  border: none;
  border-radius: 8px;
}



/* MEDIA QUERIES */
@media screen and (max-width: 600px) {
  .container {
      width: 90%;
  }
}
</style>
