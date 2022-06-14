<template>
<div>
    <div>
        <div class="post">
            <div><strong>Название: </strong>{{post.title}}</div>
            <div><strong>Описание: </strong>{{post.body}}</div>
        </div>
    </div>
    <div class="post__btns">
        <my-button @click="$emit('remove', post)" class="btn btn__inside">Delete</my-button>
    </div>

</div>
       
</template>

<script>
    export default {
        props: {
            post: {
                type: Object,
                required: true,
            },
        }
    }
</script>

<style>

    .post__btns {
        display: flex;
        align-items: center;
        justify-content: center;
    }

</style>