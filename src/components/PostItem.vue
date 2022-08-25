<template>
  <div class="post">
    <div>
      <div><strong>Название: </strong>{{ post.title }}</div>
      <div><strong>Описание: </strong>{{ post.body }}</div>
    </div>
    <div class="post__btns">
      <my-button class="button" @click="$emit('remove', post)">Удалить</my-button>
      <my-button class="button" @click="$router.push(`/posts/${post.id}`)">Открыть</my-button>
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton";
export default {
  name: "PostItem",
  components: {MyButton},
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped lang="scss">

.post{
  padding: 15px;
  border: 2px solid darkslateblue;
  margin-top: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.post__btns{
  display: flex;
  flex-direction: column;
}

.button{
  width: 80px;
  margin-top: 4px;
}

</style>