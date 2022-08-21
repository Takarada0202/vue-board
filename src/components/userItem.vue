<template>
    <div v-if="type == 0">
        <div v-for="(user, idx) in userList" :key="idx">
            <router-link :to="{name : 'board', params: {id : user.userId}}">{{user.userId}}</router-link>
        </div>
    </div>
    <div v-if="type == 1 ">
            <input type="radio" value="null"  name="compl" v-model="completed" > 
            <input type="radio" value="true" name="compl" v-model="completed" >
            <input type="radio" value="false" name="compl" v-model="completed">
        <ul v-for="(board,idx) in data" :key="idx">
            <li v-if="board.userId==this.propsUserId && this.completed == null">{{board.title}}</li>
            <li v-else-if="board.userId==this.propsUserId && board.completed ==this.completed">{{board.title}}</li>
        </ul>
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
            completed : true,
        }
    },
    props :{
        type : Number,
        propsUserId : Number,
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


    }

    


</script>

<style>

</style>