<template>
    <div v-if="posts.length > 0">
        <h3>Список постов</h3>
        <transition-group name="post-list">
            <post-item
            v-for="post in posts"
            class="post"
            :post="post"
            :key="post.id"
            @remove='$emit("remove", post)'
            />
        </transition-group>
    </div>
            <h2 v-else style="color:red">
            Список постов пуст!
        </h2>

</template>

<script>
import PostItem from "../Components/PostItem.vue";
export default {
    components: {
        PostItem,
    },
    props: {
        posts: {
            type: Array,
            required: true,
        },
    }, 
    data() {

    },
    methods: {
        
    },
}



</script>

<style scoped>
.post {
    padding: 15px;
    border: 2px solid rgba(125, 206, 164, 0.867);
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.post-list-move {
  transition: transform 1s ease;
}
    
</style>

