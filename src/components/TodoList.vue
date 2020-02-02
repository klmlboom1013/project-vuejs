<!-- 할 일 목록 표시 및 특정 할 일 삭제. -->
<template>
    <section>
        <ul>
            <li v-for="(todoItem, index) in todoItems" v-bind:key="index" class="shadow">
                <i class="checkBtn fa fa-check" aria-hidden="true"></i>
                {{ todoItem[1] }}
                <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
                    <i class="fa fa-trash-o" aria-hidden="true"></i>
                </span>
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    data() {
        return {
            todoItems: []
        }
    },
    methods: {
        removeTodo(todoItem, index){
            var key = todoItem[0];
            var val = todoItem[1];
            console.log("Remove TodoItam = {", key,":",val,"}");
            localStorage.removeItem(key);
            this.todoItems.splice(index, 1);
        }
    },
    created() {
        for(var i=0; i < localStorage.length; i++){
            var key = localStorage.key(i);
            if(key.indexOf("TODO_LIST_")!=0){
                continue;
            }
            var todoInfo = [key, localStorage.getItem(key)];
            this.todoItems.push(todoInfo);
        }
    }
}
</script>

<style>
    ul {
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0px;
        text-align: left;
    }
    
    li{
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: white;
        border-radius: 5px;
    }

    .checkBtn {
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
    }

    .removeBtn {
        margin-left: auto;
        color: #de4343;
    }
</style>