<template>
        <form @submit.prevent>
            <h4>Создание нового поста</h4>
            <my-input v-model="post.title" type="text" placeholder="Название поста"/>
            <my-input v-model="post.body" type="text" placeholder="Описание поста"/>
            <my-button @click="createPost" class="btn" style="margin-top:15px">Создать</my-button>
        </form>
</template>

<script>
export default {
    data() {
        return {
            post: {
                title: "",
                body: "",
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit("create", this.post);
            this.post = {
                title: "",
                body: "",
            }
        }
    },
}



</script>

<style scoped>

    form {
        display: flex;
        flex-direction: column;
    }

</style>

