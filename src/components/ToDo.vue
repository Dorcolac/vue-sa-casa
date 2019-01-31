<template>
    <div id="ToDo">
        <div class="form">
            <input id="checkAll" @click="checkAll()" type="checkbox">
            <input @keydown="add($event)" type="text" placeholder="What do you need to do?">
            <button type="reset">Clear list</button>
        </div>
        <ul v-for="(value, index) in tasks">
            <li>
                <input type="checkbox" :checked="value.completed">
                <span class="taskText">
                    <span :class="{ strike : value.completed }">{{ value.text }}</span>
                </span>
                <button class="close" @click="remove(index)">X</button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "ToDo",
    data () {
        return {
            tasks: [
                {text: 'This is some task', completed: true},
                {text: 'This is another task', completed: false},
                {text: 'This is some other task', completed: true},
                {text: 'This is yet another task', completed: false}
            ],
            add(event) {
                if (event.key === "Enter") {
                    this.tasks.push({text: 'new task', completed: false});
                    
                }
            },
            remove(index) {
                this.tasks.splice(index, 1);
            },
            checkAll() {
                if (document.getElementById('checkAll').checked == true) {
                    for (let i = 0; i < this.tasks.length; i++) {
                        this.tasks[i].completed = true;
                    }
                }
                else {
                    for (let i = 0; i < this.tasks.length; i++) {
                        this.tasks[i].completed = false;
                    }
                }
            }
        }
    }
}
</script>

<style>
    .form,
    ul li {
        padding: 10px;
        width: 500px;
        margin: 0 auto;
    }

    .form {
        background-color: #eee;
    }

    input[type="text"] {
        width: 70%;
        height: 34px;
        padding: 0;
    }

    .form input[type="checkbox"] {
        position: relative;
        left: -15px;
    }

    button {
        background-color: #fff;
        border: 1px solid gray;
        height: 40px;
        padding: 0 20px;
        display: block;
        float: right
    }

    ul {
        list-style-type: none;
        padding: 0;
        margin: 0;
    }

    li {
        display: flex;
        justify-content: space-between;
        background-color: rgb(50, 116, 192);
        color: #fff;
        font-weight: bold;
        border-bottom: 1px solid #fff;
    }

    li:nth-last-of-type() {
        border-bottom: none;
    }

    .taskText {
        width: 86%;
        text-align: left
    }

    .close {
        visibility: visible;
        transition: .6s;
        padding: 0;
        margin: 0;
        background-color: transparent;
        height: auto;
        border: none;
        color: white;
    }    

    .strike {
        text-decoration: line-through;
    }

</style>
