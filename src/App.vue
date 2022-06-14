<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <my-input
        v-model="searchQuery"
        placeholder="Search posts ... "
        />
        <div class="app__btns">
            <my-button @click="showDialog">Добавить пост</my-button>
            <my-select
            v-model="selectedSort"
            :options="sortOptions"/>
        </div>
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost"/>
        </my-dialog>
        <post-list :posts="sortedAndSearchedPosts" @remove="removePost" v-if="!isPostsLoading"/>
        <div v-else>Loading ...</div>
    </div>
</template>


<script>
import PostList from "./Components/PostList.vue";  
import PostForm from "./Components/PostForm.vue";
import MySelect from "./Components/UI/MySelect.vue";
import MyButton from "./Components/UI/MyButton.vue";
import axios from "axios";

    export default {

        components: {
    PostForm,
    PostList,
    MySelect,
    MyButton,
},

        data() {
            return {
                posts: [],
                dialogVisible: false,
                isPostsLoading: false,
                selectedSort: '',
                searchQuery: '',
                page: 1,
                limit: 10,
                totalPages: 0,
                sortOptions: [
                    {value: 'title', name: "By name"},
                    {value: 'body', name: "By descr"}
                ]
            }
        },
        methods: {
            createPost(post) {
               this.posts.push(post);
               this.dialogVisible = false;
            },
            removePost(post) {
               this.posts = this.posts.filter(p => p.id !== post.id);
            },
            showDialog(){
                this.dialogVisible = true;
            },
            async fetchPosts() {
                try {
                    this.isPostsLoading = true;
                    const response = await axios.get("https://jsonplaceholder.typicode.com/posts", {
                        params: {
                            _page: this.page,
                            _limit: this.limit,

                        }
                    }); 
                    this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
                    this.posts = response.data;
                    
                } catch (error) {
                    alert('Error occured!')
                } finally {
                    this.isPostsLoading = false;
                }
            }
        },
        mounted() {
            this.fetchPosts();
        },
        computed: {
            sortedPost() {
                return[...this.posts].sort((post1,post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]));
            },
            sortedAndSearchedPosts(){
                    return this.sortedPost.filter(post => post.body.toLowerCase().includes(this.searchQuery.toLowerCase()));
            }
        }
    }
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.app {
    padding: 20px;
}

.app__btns {
    display: flex;
    justify-content: space-between;
    margin: 15px 0;
}

</style>