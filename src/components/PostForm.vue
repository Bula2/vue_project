<template>
  <form class="form" @submit.prevent>
    <h3>Добавление поста</h3>
    <my-input v-focus v-model="newPost.title" type="text" placeholder="Название"/>
    <my-input v-model="newPost.body"  type="text" placeholder="Описание"/>
    <my-button style="margin-top: 10px" @click="createPost">Добавить</my-button>
  </form>
</template>

<script>
import MyInput from "@/components/UI/MyInput";
import MyButton from "@/components/UI/MyButton";
export default {
  name: "PostForm",
  components: {MyButton, MyInput},
  props: {
    posts: {
      type: Array,
      required: true
    },
    show: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      newPost: {
        title: "",
        body: ""
      }
    }
  },
  methods: {
    createPost() {
      this.newPost.id = this.posts.length;
      this.newPost.title && this.newPost.body && this.$emit("create", this.newPost);
      if (this.newPost.title && this.newPost.body) {
        this.newPost = {
          title: "",
          body: ""
        }
        this.$emit("update:show", false);
      }
    }
  }
}
</script>
<style scoped lang="scss">
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

</style>