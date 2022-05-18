<template>
    <div :class="[task.reminder ? 'reminder' : '', 'task']">
        <h3>
            {{ task.text }}
            <i class="fa-solid fa-delete-left" @click="onDelete(task.id)"></i>
        </h3>
        <p>
            {{ task.day }}
            <i
                :class="[
                    task.reminder
                        ? 'fa-solid fa-bell-slash'
                        : 'fa-solid fa-bell',
                ]"
                @click="onToggle(task.id)"
            ></i>
        </p>
    </div>
</template>

<script>
export default {
    name: 'TaskComp',
    props: {
        task: Object,
    },
    methods: {
        onDelete(id) {
            this.$emit('delete-task', id);
        },
        onToggle(id) {
            this.$emit('toggle-reminder', id);
        },
    },
};
</script>

<style scoped>
i {
    cursor: pointer;
}
.task {
    background-color: #f4f4f4;
    color: #000;
    padding: 10px;
    border-radius: 5px;
    width: 80%;
    margin: auto;
}

.task.reminder {
    border-left: 5px solid green;
}
.task h3 {
    font-weight: bold;
    font-size: 14px;
    display: flex;
    justify-content: space-between;
}

.task p {
    font-size: 12px;
    display: flex;
    margin-top: 20px;
    justify-content: space-between;
}
</style>
