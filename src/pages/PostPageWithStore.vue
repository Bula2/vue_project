<template>
  <div>
    <div class="header-container">
      <h2 class="header">Страница с постами</h2>
      <router-link to="/">На главную</router-link>
    </div>
    <my-input
        :model-value="searchQuery"
        @update:model-value="setSearchQuery"
        placeholder="Поиск..."
        v-focus
    />
    <div class="app__buttons">
      <my-button class="app__button" @click="showDialog">Создать пост</my-button>
      <my-select
          :model-value="selectedSort"
          @update:model-value="setSelectedSort"
          :options="sortOptions"
      />
    </div>

    <my-dialog v-model:show="dialogsVisible">
      <post-form v-model:show="dialogsVisible" :posts="posts" @create="createPost"/>
    </my-dialog>

    <post-list v-if="!isPostsLoading" @remove="removePost" :posts="sortedAndSearchedPosts"/>

    <div class="loading" v-else>Идет загрузка...</div>
    <div v-intersection="loadMorePosts" class="observer"></div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from "@/components/UI/MyDialog";
import MyButton from "@/components/UI/MyButton";
import MySelect from "@/components/UI/MySelect";
import MyInput from "@/components/UI/MyInput";
import {mapState, mapGetters, mapActions, mapMutations} from "vuex"

export default {
  name: "PostPage",
  components: {MyButton, MySelect, MyInput, MyDialog, PostForm, PostList},
  data() {
    return {
      dialogsVisible: false
    }
  },
  methods: {
    ...mapMutations({
      setPage: "post/setPage",
      setSearchQuery: "post/setSearchQuery",
      setSelectedSort: "post/setSelectedSort",
      setPosts: "post/setPosts"
    }),
    ...mapActions({
      loadMorePosts: "post/loadMorePosts",
      fetchPosts: "post/fetchPosts"
    }),
    createPost(newPost) {
      newPost.title && newPost.body && this.posts.unshift(newPost);
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    showDialog() {
      this.dialogsVisible = true;
    }
  },
  mounted() {
    this.fetchPosts()
  },
  computed: {
    ...mapState({
      posts: state => state.post.posts,
      isPostsLoading: state => state.post.isPostsLoading,
      selectedSort: state => state.post.selectedSort,
      searchQuery: state => state.post.searchQuery,
      page: state => state.post.page,
      limit: state => state.post.limit,
      totalPage: state => state.post.totalPage,
      sortOptions: state => state.post.sortOptions
    }),
    ...mapGetters({
      sortedPosts: "post/sortedPosts",
      sortedAndSearchedPosts: "post/sortedAndSearchedPosts"
    })

  },
  watch: {}
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

.header-container {
  display: flex;
  justify-content: space-between;
}

.app__buttons {
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
}

.app__button {
  height: 40px;
  margin-right: 10px;
}

.loading {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  font-size: 1.4em;
}

.page__wrapper {
  display: flex;
  justify-content: center;
  margin-top: 15px;
}

.page {
  display: flex;
  justify-content: center;
  width: 36px;
  border: 1px solid black;
  padding: 10px;

  &:hover {
    background: #bbffff;
  }
}

.current-page {
  background: #bbffff;
}

.observer {
  height: 30px;
}

</style>