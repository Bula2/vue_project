<template>
 <div class="about">
   <h1>Данное приложение создано для публикации и чтения постов по IT тематике!</h1>
   <router-link to="/">На главную</router-link>
 </div>
</template>

<script>
export default {
  name: "AboutPage"
}
</script>

<style scoped lang="scss">
  .about{
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
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