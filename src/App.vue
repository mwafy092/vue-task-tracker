<template>
    <div class="container">
        <HeaderComp title="Task Tracker" />
    </div>
</template>

<script>
import HeaderComp from './components/HeaderComp.vue';

export default {
    name: 'App',
    components: {
        HeaderComp,
    },
};
</script>

<style>
* {
    font-family: Arial, Helvetica, sans-serif;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
.container {
    width: 70vw;
    height: 100vh;
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
}
</style>
