<template>
    <div>
        <BaseInputText
            :inputText="editText"
            @addTodo="addTodo"
            @removeAll="removeAll"
            @updateTodo="updateTodo"
        />
        <ul>
            <li is="TodoListItem"
                v-for="todo in todos"
                :key="todo.id"
                :todo="todo"
                @remove="remove"
                @edit="edit">
            </li>
        </ul>
    </div>
</template>

<script>
import BaseInputText from './BaseInputText'
import TodoListItem from './TodoListItem'

let newTodoId = 1;

export default {
    name: 'TodoList',
    components: {
        BaseInputText,
        TodoListItem
    },
    data() {
        return {
            todos: [],
            editText: '',
            editId: -1
        }
    },
    methods: {
        addTodo: function(text) {
            const trimmedText = text.trim();
            if (trimmedText) {
                this.todos.push({
                    id: newTodoId++,
                    text: trimmedText
                });
            }
        },
        remove: function(id) {
            let index = this.todos.findIndex(item => {
                return item.id === id;
            });
            this.todos.splice(index, 1);
        },
        removeAll: function() {
            this.todos.splice(0, this.todos.length);
        },
        edit: function(id) {
            let todo = this.todos.find(item => {
                return item.id === id;
            });
            this.editText = todo.text;
            this.editId = todo.id;
        },
        updateTodo: function(text) {
            const trimmedText = text.trim();
            if (trimmedText) {
                if (this.editText) {
                    let index = this.todos.findIndex(item => {
                        return item.id === this.editId;
                    });
                    this.todos.splice(index, 1, {
                        text: text,
                        id: this.editId
                    });
                }
            }
            this.editText = '';
            this.editId = -1;
        }
    }
}
</script>

<style scoped>
ul {
    padding: 0;
}
</style>


