<style scoped>
*{ box-sizing: border-box; }
ul { margin: 0; padding: 0; }
ul li {
    cursor: pointer; position: relative; padding: 8px 8px 8px 40px;
    background: #eee; font-size: 14px; transition: .2s;
    -webkit-user-select: none; -moz-user-select: none;
    -ms-user-select: none; user-select: none;
}

ul li:hover { background: #ddd; }
ul li.checked {
    background: #BBB; color: #fff; text-decoration: line-through;
}

ul li.checked::before {
    content: ''; position: absolute; border-color: #fff;
    border-style: solid; border-width: 0px 1px 1px 0px;
    top: 10px; left: 16px; transform: rotate(45deg);
    height: 8px; width: 8px;
}

.close {
    position: absolute; right: 0; top: 0;
    padding: 8px 12px 8px 12px
}

.close:hover {
    background-color: #f44336; color: white;
}
</style>

<template>
    <ul id ="todolist">
        <li v-for="a in todolist" :key="a.id" :class="checked(a.done)"
            @click="doneToggle(a.id)">
            <span>{{ a.todo }}</span>
            <span v-if="a.done"> (완료) </span>
            <span class="close" v-on:click.stop="deleteTodo(a.id)">&#x00D7;</span>
        </li>
    </ul>
</template>

<script>
import eventBus from './EventBus.vue'

export default {
    created: function() {
        eventBus.$on('add-todo', this.addTodo);
    },
    data: function() {
        return {
            todolist : [
                {id:1, todo: "영화보기", done: false},
                {id:2, todo: "주말산책", done: true},
                {id:3, todo: "ES6 학습", done: false},
                {id:4, todo: "잠실야구장", done: false},
            ]
        }
    },
    methods : {
        checked: function(done) {
            if(done) return { checked:true };
            else return { checked:false };
        },
        addTodo: function(todo) {
            if (todo !== "") {
                this.todolist.push(
                    { id:new Date().getTime(), todo: todo, done:false });
            }
        },
        doneToggle: function(id) {
            var index = this.todolist.findIndex((item) => item.id === id);
            this.todolist[index].done = !this.todolist[index].done;
        },
        deleteTodo: function(index) {
            var index = this.todolist.findIndex((item) => item.id === id);
            this.todolist.splice(index, 1);
        }
    }
}
</script>