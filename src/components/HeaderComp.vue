<template>
    <header>
        <h1>{{ title }}</h1>
        <ButtonComp text="Add Task" color="green" />
    </header>
</template>

<script>
import ButtonComp from './ButtonComp.vue';

export default {
    name: 'HeaderComp',
    props: {
        title: String,
    },
    components: {
        ButtonComp,
    },
};
</script>

<style>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    margin-bottom: 2rem;
}
</style>
