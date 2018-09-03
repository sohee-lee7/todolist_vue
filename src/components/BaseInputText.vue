<template>
    <div>
        <input 
            type="text"
            class="input"
            v-model="value"
            @keydown.enter="updateTodo"
        >
        <button class="btn-add" @click="updateTodo">Add</button>
        <button class="btn-edit btn-hide" @click="updateTodo">Edit</button>
        <button @click="clearInputText">Clear</button>
        <button @click="removeAll">Remove All</button>
    </div>
</template>

<script>
export default {
    props: {
        inputText: {
            type: String
        }
    },
    data() {
        return {
            value: '',
            mode: 'add'
        }
    },
    watch: {
        inputText: function(text) {
            if (text) {
                this.value = text;
                this.mode = 'edit';
            } else {
                this.mode = 'add';
            }
        },
        mode: function() {
            let btnAdd = this.$el.getElementsByClassName('btn-add')[0];
            let btnEdit = this.$el.getElementsByClassName('btn-edit')[0];
            if (this.mode === 'add') {
                btnAdd.classList.remove('btn-hide');
                btnEdit.classList.add('btn-hide');
            } else if (this.mode === 'edit') {
                btnAdd.classList.add('btn-hide');
                btnEdit.classList.remove('btn-hide');
            }
        }
    },
    methods: {
        updateTodo: function() {
            if (this.mode === 'add') {
                this.$emit('addTodo', this.value);
            } else if (this.mode === 'edit') {
                this.$emit('updateTodo', this.value);
            }
            this.value = '';
        },
        clearInputText: function() {
            this.value = '';
        },
        removeAll: function() {
            this.$emit('removeAll');
        }
    }
}
</script>

<style scoped>
.input {
    width: 300px;
    height: 20px;
}
.btn-hide {
    display: none;
}
</style>
