<template>
  <div v-if="posts.length>0">
    <transition-group name="post-list">
      <post-item
          v-for="post in posts"
          :key="post.id"
          :post="post"
          @remove="$emit('remove', post)"
      />
    </transition-group>
  </div>
  <div v-else class="no_posts">
    <h2>Список постов пуст</h2>
  </div>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  name: "PostList",
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped lang="scss">

.no_posts {
  color: orangered;
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active, .post-list-leave-active {
  transition: all .5s;
}
.post-list-enter-from, .post-list-leave-to {
  opacity: 0;
  transform: translateX(230px);
}

.post-list-move{
  transition: transform 0.5s ease;
}

</style>