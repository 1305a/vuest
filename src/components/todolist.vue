<template>
    <div>
        <ul>
            <todoitem 
                v-for="(todo, i) of todos"
                v-bind:todo="todo"
                v-bind:index="i"
                v-on:remove-todo="removetodo"
            />
        </ul>
    </div>
</template>

<script>
import todoitem from '@/components/todoitem'
export default {
    props: ['todos'],
    components: {
        todoitem
    },
    methods: {
        removetodo(id) {
            this.$emit('remove-todo', id)
        }
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>