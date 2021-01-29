<template>
  <div class="wrapper">
    <h1>{{ title }}</h1>
    <NuxtLink to="/">Back</NuxtLink>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: ["title"]
}
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  border: 1px solid var(--white);
}

.wrapper h1 {
  font-family: var(--sketch);
  padding: 8px 0 8px 12px;
}

.wrapper a {
  text-decoration: none;
  color: var(--white);
  border-left: 1px solid #f7f7f7;
  font-weight: bold;
  padding: 18px 24px;
  transition: all .3s ease;
}

.wrapper a:hover {
  color: var(--dark);
  background-color: #f7f7f7;
}
</style>