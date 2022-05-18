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
