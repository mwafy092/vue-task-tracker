<template>
    <div class="container">
        <HeaderComp
            title="Task Tracker"
            @toggle-add-task="toggleAddTask"
            :showAddTask="showAddTask"
        />
        <div v-show="showAddTask" class="add-task-container">
            <AddTaskComp @add-task="addTask" />
        </div>
        <TasksComp
            :tasks="tasks"
            @delete-task="deleteTask"
            @toggle-reminder="toggleReminder"
        />
    </div>
</template>

<script>
import HeaderComp from './components/HeaderComp.vue';
import TasksComp from './components/TasksComp.vue';
import AddTaskComp from './components/AddTaskComp.vue';

export default {
    name: 'App',
    data() {
        return {
            tasks: [],
            showAddTask: false,
        };
    },
    methods: {
        addTask(task) {
            console.log(task);
            this.tasks = [...this.tasks, task];
        },
        deleteTask(id) {
            if (confirm('Are you sure?')) {
                this.tasks = this.tasks.filter((task) => task.id !== id);
            }
        },
        toggleReminder(id) {
            this.tasks = this.tasks.map((task) =>
                task.id === id ? { ...task, reminder: !task.reminder } : task
            );
        },
        toggleAddTask() {
            this.showAddTask = !this.showAddTask;
        },
        async fetchTasks() {
            const res = await fetch('http://localhost:4000/tasks');
            const data = await res.json();
            return data;
        },
    },
    async created() {
        this.tasks = await this.fetchTasks();
    },
    components: {
        HeaderComp,
        TasksComp,
        AddTaskComp,
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
.add-task-container {
    margin: auto;
    width: 100%;
}
</style>
