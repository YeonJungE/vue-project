<template>
    <div>
        <ul id="myUL">
            <li v-for="(todoItem, index) in propsItems" v-bind:key="todoItem.content">
                <input type="checkbox" v-on:click="toggleComplete(todoItem, index)" :checked="todoItem.completed">
                <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.content }}</span>
                <button v-on:click="itemRemove(todoItem, index)"> X </button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: [
        'propsItems'
    ],
    methods: {
        itemRemove(todoItem, index) {
            this.$emit('itemRemove', todoItem, index);
        },
        toggleComplete: function(todoItem, index) {
            this.$emit('toggleComplete', todoItem, index);
        },
    }
}
</script>

<style scoped>
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
</style>
