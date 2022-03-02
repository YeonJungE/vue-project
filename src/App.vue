<template>
  <div id="app">
    <ListHeader></ListHeader>
    <ListInput v-on:addTodoItem="addTodoItem"></ListInput>
    <List v-bind:propsItems="todoItems" v-on:itemRemove="todoItemRemove" v-on:toggleComplete="todoItemComplete"></List>
    <ListFooter v-on:todoListAllClear="todoItemAllClear"></ListFooter>
  </div>
</template>

<script>
import ListHeader from './components/TodoListHeader';
import ListFooter from './components/TodoListFooter';
import List from './components/TodoList';
import ListInput from './components/TodoListInput';

export default {
  components: {
    'ListHeader': ListHeader,
    'ListFooter': ListFooter,
    'List': List,
    'ListInput': ListInput,
  },
  //  데이터 초기화
  data() {
      return {
          todoItems: [],
      }
  },
  created() {
    // 데이터 셋팅
    if (localStorage.length > 0) {
        for(var i=0; i<localStorage.length; i++) {
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
    }
  },
  methods: {
    addTodoItem(todoItem) { // 입력받은 값 저장
          var todoItemData = {
              content: todoItem,
              completed: false
          };

          localStorage.setItem(todoItem, JSON.stringify(todoItemData));
          this.todoItems.push(todoItemData);
    },
    todoItemRemove(todoItem, index) { // 해당 글 삭제
        localStorage.removeItem(todoItem.content);
        this.todoItems.splice(index, 1);
    },
    todoItemComplete(todoItem) {  
      // 체크박스 반대로 저장  (완료 => 비완료 / 비완료=>완료)
      todoItem.completed =  !todoItem.completed;
      localStorage.setItem(todoItem.content, JSON.stringify(todoItem));
    },
    todoItemAllClear() { // 전체삭제
      localStorage.clear();
      this.todoItems = [];
    }
  }
}
</script>

