<template>
    <div class="main">
      <h1>Добро пожаловать!</h1>
      <router-link to="/posts">К постам</router-link>
      <router-link to="/about">О нас</router-link>
<!--      <router-link to="/store">К стору</router-link>-->
    </div>
</template>

<script>
export default {
  name: "MainPage"
}
</script>

<style scoped lang="scss">
  .main{
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  a{
    margin-top: 10px;
    text-decoration: none;
    color: black;
    font-size: 1.8em;
    &:hover{
      color: #0b0efa;
    }
  }
</style>