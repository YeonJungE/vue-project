<template>
    <button v-on:click="allClear()">전체 삭제</button>
</template>

<script>
export default {
    methods: {
        allClear() {
            this.$emit('todoListAllClear');
        }
    }
}
</script>
