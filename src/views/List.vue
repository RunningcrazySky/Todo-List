<template>
    <div class="box">
        <div class="title">
            <div class="left">
                <div class="add" @click='onAdd'>
                    +
                </div>
                <div class="name">
                    Todo List
                </div>
            </div>
            <div class="right">
                <button class="selectall" @click="onSelectAll()">
                    全选
                </button>
                <button class="addlist" @click='onAdd'>
                    添加
                </button>
            </div>
        </div>
        <!-- 条目 -->
        <div class="content">
            <ul>
                <!-- eslint-disable-next-line -->
                <li v-for="(item, index) in todoList" :key="item.id">
                    <div class="left">
                        <!-- 复选框 -->
                        <input 
                        type="checkbox" 
                        @click="onSelected(index, item.id)"
                        :checked="item.isCheck"
                        >
                        <!-- input输入框 -->
                        <input 
                        type="text" 
                        placeholder="请点击上方的添加按钮添加事件" 
                        v-model="item.text"
                        :disabled='item.isCheck'
                        :class="item.isCheck ? 'line-through' : ''"
                        @blur="onBlur"
                         ref='inputBox'
                        >
                    </div>
                    <div class="right">
                    <div class="time">{{item.time}}</div>
                        <button class="del" @click="onDelete(index, item.id)">
                            删除
                        </button>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import { nanoid } from 'nanoid'
import dayjs from 'dayjs'
    export default {
        name:'Title',
        data(){
            return{
                todoList:[],
            }
        },
        // 获取本地存储
        created(){
            if(this.todoList){
                this.todoList = JSON.parse(window.localStorage.getItem('ListTodo'))
            }else{
                this.todoList = [{
                    id: nanoid(),
                    isCheck: false, // 是否选中
                    text: '',
                    time: dayjs().format('YY-MM-DD HH:MM'),
                }]
            }
        },
        methods:{
            // 添加功能
            onAdd(){
                this.todoList.unshift({
                    id: nanoid(),
                    isCheck: false, // 是否选中
                    text: '',
                    time: dayjs().format('YY-MM-DD hh:mm'),
                })
                this.$nextTick(()=>{
                    this.$refs.inputBox[this.todoList.length - 1].focus()
                })
            },
            // 删除功能
            onDelete(index, id){
                if(this.todoList[index].id === id){
                    this.todoList.splice(index, 1)
                    this.storage()
                }
            },
            // 单选功能
            onSelected(index, id){
                if(this.todoList[index].id === id){
                    this.todoList[index].isCheck = !this.todoList[index].isCheck
                    console.log(this.todoList[index].isCheck)
                    this.storage()
                }
            },
            // 全选功能
            onSelectAll(){
                this.todoList.forEach(item => {
                    item.isCheck = !item.isCheck
                    this.storage()
                });
            },
            // 本地存储
            storage(){
                window.localStorage.setItem('ListTodo', JSON.stringify(this.todoList))
            },
            // 输入完毕
            onBlur(){
                this.storage()
            }
        }
    }
</script>

<style lang='less' scoped>
    *{
        padding: 0;
        margin: 0;
        .box{
            box-sizing: border-box;
            width: 500px;
            margin: 50px auto;
            border-radius: 5px;
            background-color: pink;
            text-align: center;
        }
    }
    .title{
        display: flex;
        justify-content: space-between;
        padding: 20px;
        border-bottom: 1px solid white;
        .left{
            display: flex;
            justify-content: space-between;
            align-content: center;
            .add{
                width: 30px;
                border-radius: 50%;
                background-color: white;
                text-align: center;
                vertical-align: middle;
                margin-right: 10px;
                font-weight: 600;
                cursor: pointer;
                &:hover{
                    background: #000;
                    color: white;
                }
            }
        }
        .right{
                button{
                    border-style: none;
                    font-size: 16px;
                    background-color: orange;
                    font-size: 14px;
                    padding: 5px 10px;
                    border-radius: 5px;
                    color: white;
                    cursor: pointer;
                }
                .addlist{
                    margin-left: 5px;
                    background-color: green;
                }
            }
    }
    // 隐藏滚动条
    .content::-webkit-scrollbar {display:none}
    .content{
        height: 400px;
        padding: 10px 8px;
        overflow: scroll;
        li{
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 5px;
            margin-bottom: 5PX;
            background: rgba(255, 255, 255, 0.5);
            font-size: 12px;
            input{
                border: none;
                outline: none;
                background: transparent;
                border-bottom: 1px solid pink;
                font-size: 14px;
                &::placeholder{
                    font-size: 14px;
                }
            }
            input[type='text']{
                width: 250px;
                margin-left: 10px;
            }
            .right{
                display: flex;
                justify-content: space-between;
                align-items: center;
                button{
                    border: 0;
                    cursor: pointer;
                    background: red;
                    color: white;
                    padding: 5px 8px;
                    border-radius: 5px;
                    font-size: 14px;
                    margin-left: 5px;
                }
            }
        }
    }
    .line-through{
                    color: gray;
                    text-decoration: line-through white;
                }
</style>