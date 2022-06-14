<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>
export default {
  name: 'my-button'
}
</script>

<style>
    .btn {
        align-self: flex-end;
        padding: 10px 20px;
        background: none;
        border: 1px solid rgba(125, 206, 164, 0.867);
        color: rgba(125, 206, 164, 0.867);
        transition: all 0.4s ease;
        cursor: pointer;
    }

    .btn:hover {
        background-color: rgba(125, 206, 164, 0.867);
        color: white;
    }

</style>