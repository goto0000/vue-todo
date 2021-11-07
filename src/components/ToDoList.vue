<template>
    <div>
        <input v-model="inputValue">
        <br>
        <button v-on:click="handleClick">
            ToDoを追加
        </button>
        <br>
        <input
            v-model="filterValue"
            placeholder="フィルタテキスト">
        <ul>
            <!-- <li
                v-for="todo in filteredTodoItems"
                v-bind:key="todo.id"
                class="todo-item"
                v-bind:class="{'done': todo.done}"
                v-on:click="todo.done = !todo.done">
                <span v-if="todo.done">✅</span>{{ todo.text }} -->
            <!-- </li> -->
            <!-- <ToDoItem
                v-for="todo in filteredTodoItems"
                v-bind:key="todo.id"
                v-bind:text="todo.text"
                v-bind:done="todo.done"
                v-on:toggle="todo.done = !todo.done"
            /> -->
            <ToDoItem
                v-for="todo in filteredTodoItems"
                v-bind:key="todo.id"
                v-bind:done="todo.done"
                v-on:toggle="todo.done = !todo.done">
                {{ todo.text }}
            </ToDoItem>
        </ul>
    </div>
</template>

<script>
import _ from "lodash"
import ToDoItem from './ToDoItem.vue'
export default {
    components: { ToDoItem },
    data() {
        const todoItems = [
            {id: 1, done: false, text: 'Go out to sea'},
            {id: 2, done: false, text: 'Invite the first member'},
        ];
        return {
            inputValue: '',
            todoItems,
            filterValue: '',
            filteredTodoItems: todoItems,
        }
    },
    /*
    computed: {
        filteredTodoItems() {
            if (!this.filterValue) {
                return this.todoItems
            }
            return this.todoItems.filter(todo => {
                return todo.text.includes(this.filterValue)
            })
        }
    },
    */
    watch: {
        filterValue() {
            this.updatefilteredTodoItems()
        },
        todoItems: {
            handler() {
                this.updatefilteredTodoItems()
            },
            deep: true,
        },
    },
    methods: {
        handleClick() {
            // 入力をリストに追加
            this.todoItems.push({
                id: this.todoItems.length + 1,
                text: this.inputValue,
            })
            // 入力をクリアする
            this.inputValue = ''
        },
        updatefilteredTodoItems: _.debounce(function() {
            this.filteredTodoItems = this.filterValue
                ? this.todoItems.filter(todo => {
                    return todo.text.includes(this.filterValue)})
                : this.todoItems
        }, 500)
    }
}
</script>

<style>
.todo-item.done {
    background-color: #3fb983;
    color: #ffffff;
}
</style>
