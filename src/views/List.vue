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
                <button class="selectall">
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
                <li v-for="item in todoList" :key="item.id">
                    <div class="left">
                        <input type="checkbox" name="" id="">
                        <input type="text" placeholder="请点击上方的添加按钮添加事件" v-model="item.text">
                    </div>
                    <div class="right">
                    <div class="time">{{item.time}}</div>
                        <button class="del">
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
                todoList:[]
            }
        },
        methods:{
            // 添加功能
            onAdd(){
                this.todoList.push({
                    id: nanoid(),
                    isCheck: false, // 是否选中
                    text: '',
                    time: dayjs().format('YY-MM-DD HH:MM'),
                })
            },

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
</style>