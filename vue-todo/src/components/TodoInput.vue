<template>
  <div>
    <!-- v-model input입력값 동적으로 매핑해주는역할 -->
    <div class="inputbox shadow">
      <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
      <!-- <button v-on:click="addTodo">add</button> -->
      <span class="addContainer" v-on:click="addTodo">
        <font-awesome-icon icon="fa-solid fa-plus " class="addBtn"/>
      </span>
      <Modal v-if="showModal" @close="showModal = false">
        <h3 slot="header">
          경고!
          <font-awesome-icon icon="fa-solid fa-times" class="closeModalBtn" @click="showModal = false"></font-awesome-icon>
        </h3>
        <!--    Quiz body,footer 재정의    -->
        <div slot="body">
          아무것도 입력하지 않으셨습니다.
        </div>
        <div slot="footer">
          @copy right
        </div>
      </Modal>
    </div>
  </div>

</template>

<script>
import Modal from "./common/Modal.vue";

export default {
  data: function(){
    return{
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo: function() {
      // 저장하는 로직
      // Application -> Storage -> LocalStorage
      if(this.newTodoItem !== ''){
        //this.$emit(이벤트 이름, this.newTodoItem);
        this.$emit('addTodoItem',this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput: function(){
      this.newTodoItem = '';
    },
  },
  components: {
    Modal: Modal
  },
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputbox{
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputbox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer{
  float: right;
  background: linear-gradient(to right, #6478FB, #9873FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn{
  color: #42b983;
}
</style>
