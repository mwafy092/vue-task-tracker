<template>
    <div class="container">
        <HeaderComp title="Task Tracker" />
        <TasksComp :tasks="tasks" @delete-task="deleteTask" />
    </div>
</template>

<script>
import HeaderComp from './components/HeaderComp.vue';
import TasksComp from './components/TasksComp.vue';

export default {
    name: 'App',
    data() {
        return {
            tasks: [],
        };
    },
    methods: {
        deleteTask(id) {
            this.tasks = this.tasks.filter((task) => task.id !== id);
        },
    },
    created() {
        this.tasks = [
            {
                id: 1,
                text: 'Learn Vue',
                day: 'May 17th 9:00am',
                reminder: true,
            },
            {
                id: 2,
                text: 'Go to the gym',
                day: 'May 18th 9:00pm',
                reminder: true,
            },
            {
                id: 3,
                text: 'Play playstation',
                day: 'May 20th 5:00pm',
                reminder: false,
            },
        ];
    },
    components: {
        HeaderComp,
        TasksComp,
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

body {
    background-color: #eee;
}
.container {
    width: 80vw;
    max-width: 600px;
    height: 100vh;
    margin: auto;
    display: flex;
    align-items: flex-start;
    flex-direction: column;
    text-align: center;
    padding: 20px;
    background-color: #ffffff;
}
</style>
