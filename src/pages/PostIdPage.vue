<template>
  <div>
    <h1>Страница поста c ID = {{ $route.params.id }}</h1>
    <router-link to="/posts">Вернуться к постам</router-link>
  </div>
</template>

<script>
export default {
  name: "PostIdPage"
}
</script>

<style scoped lang="scss">
a {
  margin-top: 25px;
  text-decoration: none;
  color: black;
  font-size: 1.2em;

  &:hover {
    color: #0b0efa;
  }
}
</style>