<template>
    <form class="add-form" @submit="onSubmit">
        <div class="form-control">
            <label>Task</label>
            <input
                type="text"
                name="text"
                placeholder="Add Task"
                v-model="text"
            />
        </div>
        <div class="form-control">
            <label>Time</label>
            <input
                type="date"
                name="day"
                placeholder="Add Time"
                v-model="day"
            />
        </div>
        <div class="form-control">
            <label>Set Reminder</label>
            <input type="checkbox" name="reminder" v-model="reminder" />
        </div>
        <input type="submit" value="Submit Task" class="btn btn-block" />
    </form>
</template>

<script>
export default {
    name: 'AddTaskComp',
    data() {
        return {
            text: '',
            day: '',
            reminder: false,
        };
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();
            if (!this.text) {
                alert('Please add a task before submit!');
                return;
            }
            const newTask = {
                id: Math.floor(Math.random() * 500),
                text: this.text,
                day: this.day,
                reminder: this.reminder,
            };
            this.$emit('add-task', newTask);
            this.text = '';
            this.day = '';
            this.reminder = false;
        },
    },
};
</script>

<style scoped>
form {
    width: 100%;
    display: flex;
    justify-content: space-around;
    flex-direction: column;
    align-items: center;
    margin: auto;
    border-bottom: 4px solid #333;
    padding: 10px;
}
.form-control {
    margin: 10px 0;
}
label {
    font-size: 14px;
    font-weight: bold;
    color: #333;
    margin-right: 10px;
}

input[name='text'],
input[name='day'] {
    width: 300px;
    height: 30px;
    border: 2px solid #333;
    border-radius: 5px;
    font-size: 12px;
    padding: 5px;
}
input[type='submit'] {
    border: none;
    background-color: black;
    color: #fff;
    padding: 5px 10px;
    font-size: 12px;
    border-radius: 5px;
    cursor: pointer;
}
</style>
