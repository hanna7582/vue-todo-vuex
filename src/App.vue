<template>
  <div id="app" :class="this.$store.state.theme">
    <TodoHeader />
    <TodoInput />
    <TodoList />
    <TodoFooter />    
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  name: 'App',
  components: {
    TodoHeader, 
    TodoInput, 
    TodoList, 
    TodoFooter
  },
  computed:{
    todoList(){
      return this.$store.state.todoList;
    }
  },
  watch:{
    todoList(){
      this.$store.commit('todoListSet');  
    }
  }
}
</script>

<style lang="scss">
  #app{
    height: 100vh;
    box-sizing: border-box;
    padding: 20px;
    background: $light-gray;
    &.dark{
      background: $dark-gray;
    }
  }

</style>
