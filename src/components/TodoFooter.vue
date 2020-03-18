<template>
  <footer>
      <div class="btn-group">
        <button v-if="todoList.length!=0" @click="confirm">Remove All</button>
        <button v-if="isRemoveCompleted" @click="removeCompleted">Remove completed</button>      
      </div>
      <Modal v-if="showModal">      
        <h3 slot="header"></h3>
        <div slot="body">할일을 모두 삭제하시겠어요?</div>
        <div slot="footer" class="btn-group">
          <button class="modal-primary-button" @click="removeAll">OK</button>
          <button class="modal-default-button" @click="showModal=false">Cancel</button>
        </div>
        <!-- <template v-slot:footer>                      
          <div class="btn-group">
            <button class="modal-primary-button" @click="removeAll">OK</button>
            <button class="modal-default-button" @click="showModal=false">Cancel</button>
          </div>          
        </template> -->
      </Modal>
  </footer>
</template>

<script>
import Modal from './Modal'
export default {  
  components:{ Modal },
  data() {
    return {
      showModal:false
    }
  },
  computed: {
    todoList(){
      return this.$store.state.todoList;
    },  
    isRemoveCompleted:function(){
      var completedCount=this.todoList.filter( todo => todo.completed == true ).length;
      return completedCount ? true : false;      
    }
  },
  methods: {
    confirm:function(){
      this.showModal=true;
    },
    removeAll:function(){
      this.showModal=false;
      this.$store.commit('allDoneChange', {allDone:false});
      this.$store.commit('removeAll');
    },
    removeCompleted:function() {
      this.$store.commit('removeCompleted');
    },
  }
}
</script>

<style lang="scss" scoped>
  footer{
    width: calc(100% - 40px);
    @include pos-fix(auto, auto, 20px);
  }
  .flex{
    display: flex;
  }
  .btn-group{
    display: flex;
    button{
      width: 100%;
      height: 30px;
      background-color: #fff;
      color: $primary;
      &:last-child{border-left:1px solid $light-gray;}
      &.modal-primary-button{
          height: 30px;
          background-color: $primary;
          color: $white;
      }
    }
  }
</style>