<template>
    <div id="myDIV" class="header">
        <h2 style="margin:5px">TodoList !!</h2>
        <input type="text" id="myInput" v-model.trim="todoItem" v-on:keyup.enter="addTodoItem()">
        <button class="addBtn" v-on:click="addTodoItem()">추가</button>
    </div>
</template>

<script>
export default {
    //  데이터 초기 셋팅
    data() {
        return {
            todoItem: ''
        }
    },

    methods: {
        addTodoItem() {
            if (this.todoItem != '') {
                this.$emit('addTodoItem', this.todoItem);   // 부모 컴포넌트에 전달
                this.inputTextClear();
            }
        },
        // input 창 클리어
        inputTextClear() { 
            this.todoItem = '';
        },
    }
 }
</script>
