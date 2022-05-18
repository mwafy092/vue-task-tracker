<template>
    <button :style="{ background: color }" @click="onClick()">
        {{ text }}
    </button>
</template>

<script>
export default {
    name: 'ButtonComp',
    props: {
        text: String,
        color: String,
    },
    methods: {
        onClick() {
            this.$emit('btn-click');
        },
    },
};
</script>

<style scoped>
button {
    background-color: #000;
    color: #fff;
    border-radius: 5px;
    padding: 10px 20px;
    cursor: pointer;
    border: none;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 1px 3px 0px,
        rgba(0, 0, 0, 0.06) 0px 1px 2px 0px;
}
</style>
