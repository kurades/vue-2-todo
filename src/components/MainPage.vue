<template>
    <div class="container">
        <input type="text" placeholder="Type text here..." class="input" v-model="input" @keyup.enter="submitTask">
        <div v-for="(todo, index) in todos" :key="index" class="task-container">
            <span @click="changeState(index)" :class="[{ done: todo.isDone }, 'task']">{{ todo.task }}</span>
            <span v-if="index === 0">&lt;---Click text to mark as done</span>
            <div class="buttons">
                <div class="button edit" @click="editTask(index)">Edit</div>
                <div class="button delete" @click="deleteTask(index)">Delete</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "MainPage",
    data() {
        return {
            input: '',
            edittingTask : -1,
            todos: [{ task: 'this is a task', isDone: false }],
        }
    },
    methods: {
        submitTask: function () {
            
            if(this.edittingTask === -1){
                this.todos.push({ task: this.input, isDone: false });
            }else{
                this.todos[this.edittingTask].task = this.input;
                this.edittingTask = -1; 
            }
            this.input = '';
        },
        changeState: function (index) {
            this.todos[index].isDone = !this.todos[index].isDone
        },
        deleteTask: function (index) {
            this.todos.splice(index, 1)
        },
        editTask : function(index){
            this.input = this.todos[index].task;
            this.edittingTask = index;
        }

    },
}
</script>

<style scoped>
.container {
    width: 600px;
    margin: auto;
}

.task-container {
    text-align: start;
    display: flex;
    align-items: center;
    padding: 10px;
    justify-content: space-between;
}

.input {
    padding: 10px;
    border-radius: 10px;
    font-size: 17px;
    margin-bottom: 30px;
}

.task {
    cursor: pointer;
    font-weight: 600;
    transition: .3s;
    user-select: none;

}

.buttons {
    display: flex;
    flex-direction: row;
}

.button {
    padding: 20px;
    margin: 0 10px;
    border-radius: 10px;
    border: 2px solid silver;
    cursor: pointer;
}

.button.delete {
    background-color: crimson;
    color: white;
    border-color: white;
}

.task.done {
    text-decoration: line-through;
    opacity: .6;
}
</style>