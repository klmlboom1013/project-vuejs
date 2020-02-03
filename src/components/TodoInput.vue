<!--
모달 vue 예제 소스
https://vuejs.org/v2/examples/modal.html
-->

<!-- 할 일 입력 및 추가 -->
<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fa fa-plus" aria-hidden="true" ></i>
        </span>

        <modal v-if="showModal" @close="showModal=false">
            <h3 slot="header">경고</h3>
            <span slot="footer" @click="showModal=false">
                할 일을 입력하세요.
                <i class="closeModalBtn fa fa-times" aria-hidden="true"></i>
            </span>
        </modal>

    </div>
</template>

<script>
import Modal from './common/Modal.vue'
export default {
    data() {
        return {
            newTodoItem: '',
            showModal: false
        }
    },
    methods: {
        addTodo() {
            if(this.newTodoItem == '') {
                this.showModal = !this.showModal;
                return;
            }
            var value = this.newTodoItem && this.newTodoItem.trim();
            this.$emit('addTodo', value);
            this.clearInput();
        },
        clearInput() {
            this.newTodoItem = '';
        }
    },
    components: {
        Modal: Modal
    }
}
</script>

<style>
    input:focus{
        outline: none;
    }
    .inputBox {
        background: white;  
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input {
        border-style: none;
        font-size: 0.9rem;
    }
    .addContainer {
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block; /* inline-block; */
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn {
        color: white;
        vertical-align: middle;
    }
</style>