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
        <router-view></router-view>
        <FooterComp />
    </div>
</template>

<script>
import HeaderComp from './components/HeaderComp.vue';
import FooterComp from './components/FooterComp.vue';
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
        async addTask(task) {
            const res = await fetch('api/tasks', {
                method: 'POST',
                headers: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify(task),
            });
            const data = await res.json();
            this.tasks = [...this.tasks, data];
        },
        async deleteTask(id) {
            if (confirm('Are you sure?')) {
                const res = await fetch(`api/tasks/${id}`, {
                    method: 'DELETE',
                });
                res.status === 200
                    ? (this.tasks = this.tasks.filter((task) => task.id !== id))
                    : alert('error while deleting');
            }
        },
        async toggleReminder(id) {
            const taskToToggle = await this.fetchTask(id);
            const updatedTask = {
                ...taskToToggle,
                reminder: !taskToToggle.reminder,
            };
            const res = await fetch(`api/tasks/${id}`, {
                method: 'PUT',
                headers: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify(updatedTask),
            });

            const data = await res.json();
            this.tasks = this.tasks.map((task) =>
                task.id === id ? { ...task, reminder: data.reminder } : task
            );
        },
        toggleAddTask() {
            this.showAddTask = !this.showAddTask;
        },
        async fetchTasks() {
            const res = await fetch('api/tasks');
            const data = await res.json();
            return data;
        },
        async fetchTask(id) {
            const res = await fetch(`api/tasks/${id}`);
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
        FooterComp,
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
    height: fit-content;
    min-height: 100vh;
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
