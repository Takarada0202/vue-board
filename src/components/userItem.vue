<template>
    <div v-if="type == 0">
        <div v-for="(user, idx) in userList" :key="idx">
            <router-link :to="{name : 'board', params: {id : user.userId}}">{{user.userId}}</router-link>
        </div>
    </div>
    <div v-if="type == 1 ">
        <button @click="statusNull()" id="statusNullBtn"  value="null">모두</button>
        <button @click="statusTrue()" id="statusTrueBtn"  value="true">작성완료</button>
        <button @click="statusFalse()" id="statusFalseBtn" value="false">작성중</button>
        <ul v-for="(board,idx) in data" :key="idx">
            <li v-if="board.userId==this.propsUserId && this.completed == null">
                <router-link :to="{name : 'detail', params: {pageId : board.id, userId :board.userId }}">{{board.title}}</router-link>
            </li>
            <li v-else-if="board.userId==this.propsUserId && board.completed ==this.completed">
                <router-link :to="{name : 'detail', params: {pageId : board.id, userId : board.userId}}">{{board.title}}</router-link>
            </li>
        </ul>
    </div>
    <div v-if="type == 2">
        <h3>{{data[this.propsPageId-1].title}}</h3>
        <h4>{{data[this.propsPageId-1].id}}</h4>
        <div>
            <input type="button" @click="prefix()" value="prefix">
            <input type="button" @click="unit()" value="unit">
        </div>
    </div>
</template>

<script>
import _ from "lodash"
export default {
    data() {
        return {
            data : this.$userItem,
            userList : _.uniqBy((this.$userItem),'userId'),
            userBoardList : [],
            completed : null, 
        }
    },
    props :{
        type : Number,
        propsUserId : Number,
        propsPageId : Number,
    },
    mounted() { 
            // return this.data.filter(
            //     (user) => {
            //         let userId = user.userId

            //         if(this.userList.indexOf(userId) === -1) {
            //             this.userList.push(userId)
            //         }
            //         console.log(this.userList)
            //         return true
            // })
            
        },
    methods :{
        statusNull() {
            this.completed = document.querySelector('#statusNullBtn').value
            console.log(this.completed);
        },
        statusTrue() {
            this.completed = document.querySelector('#statusTrueBtn').value
            console.log(this.completed);
        },
        statusFalse() {
            this.completed = document.querySelector('#statusFalseBtn').value
            console.log(this.completed);
        },
        prefix() {

        },
        unit() {

        }
    }


    }

    


</script>

<style>

</style>