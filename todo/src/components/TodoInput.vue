<template lang="html">
  <div class="inputBox shoadow">

    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal =  false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">
        할 일을 입력하세요.
        <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
      </span>
    </modal>

  </div>
</template>

<script>

import Modal from './common/Modal.vue'

export default {
  data() {
    return {
      newTodoItem:'',
      showModal: false
    }
  },
  methods:{
    addTodo(){
      if (this.newTodoItem !== "") {
         // this.newTodoItem가 ''이 아니면 this.newTodoItem.trim()을 value 변수에 할당한다.
         // 자바스크립트에서는 대부분의 값들이 true/false로 표현이 될 수 있는데, 빈 값('')은 false로 취급된다.
        var value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit('addTodo', value)
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput(){
      this.newTodoItem = '';
    }
  },
  components:{
    'Modal': Modal
  }
}
</script>

<style lang="css" scoped>
  input:focus{
    outline: none;
  }
  .inputBox{
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input{
    border-style: none;
    font-size: 0.9rem;
  }
  .addContainer{
    float: right;
    background: linear-gradient(to right, #6478fb, #8763fb);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn{
    color: white;
    /* vertical-align: middle; */
  }
</style>
