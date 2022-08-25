<template>
  <div>
    <div class="header-container">
      <h2 class="header">Страница с постами</h2>
      <router-link to="/">На главную</router-link>
    </div>
    <my-input
        v-model="searchQuery"
        placeholder="Поиск..."
        v-focus
    />
    <div class="app__buttons">
      <my-button class="app__button" @click="showDialog">Создать пост</my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>

    <my-dialog v-model:show="dialogsVisible">
      <post-form v-model:show="dialogsVisible" :posts="posts" @create="createPost"/>
    </my-dialog>

    <post-list v-if="!isPostsLoading" @remove="removePost" :posts="sortedAndSearchedPosts"/>

    <div class="loading" v-else>Идет загрузка...</div>
    <div v-intersection="loadMorePosts" class="observer"></div>
    <!--    <div class="page__wrapper">-->
    <!--      <div-->
    <!--          v-for="pageNumber in totalPage"-->
    <!--          :key="pageNumber"-->
    <!--          class="page"-->
    <!--          :class="{-->
    <!--            'current-page': page === pageNumber-->
    <!--          }"-->
    <!--          @click="changePage(pageNumber)"-->
    <!--      >-->
    <!--        {{pageNumber}}-->
    <!--      </div>-->
    <!--    </div>-->
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from "@/components/UI/MyDialog";
import MyButton from "@/components/UI/MyButton";
import axios from "axios";
import MySelect from "@/components/UI/MySelect";
import MyInput from "@/components/UI/MyInput";

export default {
  name: "PostPage",
  components: {MyInput, MySelect, MyButton, MyDialog, PostForm, PostList},
  data() {
    return {
      posts: [],
      dialogsVisible: false,
      isPostsLoading: false,
      selectedSort: "",
      searchQuery: "",
      page: 1,
      limit: 10,
      totalPage: 0,
      sortOptions: [
        {value: "title", name: "По названию"},
        {value: "body", name: "По описанию"}
      ]
    }
  },
  methods: {
    createPost(newPost) {
      newPost.title && newPost.body && this.posts.unshift(newPost);
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    showDialog() {
      this.dialogsVisible = true;
    },
    // changePage(pageNUmber) {
    //     this.page=pageNUmber;
    // },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        const response = await axios.get("https://jsonplaceholder.typicode.com/posts", {
          params: {
            _page: this.page,
            _limit: this.limit
          }
        });
        this.totalPage = Math.ceil(response.headers["x-total-count"] / this.limit);
        this.posts = response.data;
      } catch (e) {
        alert("Ошибка")
      } finally {
        this.isPostsLoading = false;
      }
    },
    async loadMorePosts() {
      try {
        this.page += 1;
        const response = await axios.get("https://jsonplaceholder.typicode.com/posts", {
          params: {
            _page: this.page,
            _limit: this.limit
          }
        });
        this.totalPage = Math.ceil(response.headers["x-total-count"] / this.limit);
        this.posts = [...this.posts, ...response.data];
      } catch (e) {
        alert("Ошибка")
      }
    }
  },
  mounted() {
    this.fetchPosts();
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    // page() {
    //   this.fetchPosts();
    // }
  }
}
</script>

<style scoped lang="scss">

a{
  margin-top: 25px;
  text-decoration: none;
  color: black;
  font-size: 1.2em;
  &:hover{
    color: #0b0efa;
  }
}

.header-container{
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