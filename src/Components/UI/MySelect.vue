<template>
    <select v-model="modelValue" @change="changeOption">
        <option disabled value="">
            Choose something
        </option>
        <option v-for="option in options" :key="option.value" :value="option.value">
        {{option.name}}
        </option>
    </select>
</template>

<script>
    export default {
        name: "my-select",
        props: {
            modelValue: {
                type: String,
            },
            options: {
                type: Array,
                default: () => [],
            }
        },
        methods: {
            changeOption(event) {
                this.$emit("update:modelValue", event.target.value);
            }
        }
    }

</script>

<style scoped>
select {
    padding: 10px 20px;
    height: 100%;
}

</style>