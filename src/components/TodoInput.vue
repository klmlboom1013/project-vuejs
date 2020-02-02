<!-- 할 일 입력 및 추가 -->
<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fa fa-plus" aria-hidden="true" ></i>
        </span>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newTodoItem: ''
        }
    },
    methods: {
        addTodo() {
            if(this.newTodoItem !== '') {
                var value = this.newTodoItem && this.newTodoItem.trim();
                /*
                ### localStorage ###
                    - 브라우저의 Storage 영역에 해당 도메인으로 데이터를 저장 한다.
                    - 브라우저를 종료했다가 다시 열어 해당 도메인으로 접근하면 이전에 저장된 데이터를 재사용 가능 하다.
                */
                localStorage.setItem(value, value);
                this.clearInput();
            }
        },
        clearInput() {
            this.newTodoItem = '';
        }
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