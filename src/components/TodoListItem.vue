<template>
    <div class="todo">
        <span>{{ todo.text }}</span>
        <button @click="remove">remove</button>
        <button @click="edit">edit</button>
    </div>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        }
    },
    methods: {
        remove() {
            this.$emit('remove', this.todo.id);
        },
        edit() {
            this.$emit('edit', this.todo.id);
        }
    }
}
</script>

<style scoped>
.todo {
    margin: 5px 0px 5px 0px;
    text-align: left;
}
.todo span {
    margin-right: 10px;
}
</style>
