<template>
    <div v-for="task in tasks" :key="task.id">
        <TaskComp
            :task="task"
            @delete-task="$emit('delete-task', task.id)"
            @toggle-reminder="$emit('toggle-reminder', task.id)"
        />
    </div>
</template>

<script>
import TaskComp from './TaskComp.vue';

export default {
    name: 'TasksComp',
    props: {
        tasks: Array,
    },
    components: {
        TaskComp,
    },
    emits: ['delete-task', 'toggle-reminder'],
};
</script>

<style scoped>
div {
    margin: 10px;
    width: 100%;
}
</style>
