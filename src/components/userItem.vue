<template>
    <div v-if="type == 0">
        <div v-if="data == null">
            <p>데이터가 없습니다</p>
        </div>
        <div v-else>
            <div v-for="(user, idx) in userList" :key="idx">
                <h3>
                    <router-link :to="{name : 'board', params: {id : user.userId}}">{{user.userId}}</router-link>
                </h3>
        </div>
        </div>
    </div>
    <div v-if="type == 1 ">
        <div v-if="this.userList.map(function(d) { return d['userId']; }).indexOf(1) == -1"   >
            <h1>
                유저를 찾을 수 없습니다
            </h1>
        </div>
        <div v-else>
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
    </div>
    <div v-if="type == 2">
        <h3>{{data[this.propsPageId-1].title}}</h3>
        <h4>{{data[this.propsPageId-1].id}}</h4>
        <div>
            <input type="button" @click="prefix()" value="prefix">
            <input type="button" @click="unit()" value="unit">
            <router-link to="/">dd</router-link>
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
            nextPage : Number(this.propsPageId)+1,
            prevPage : Number(this.propsPageId)-1,
            maxPage : this.userDetailId * 20,
            userDetailId : Number(this.$route.params.id),
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
            // })\
           console.log(this.completed)

        },
    methods :{
        statusNull() {
            this.completed = document.querySelector('#statusNullBtn').value
            setTimeout(() => {
                    this.$router.go()
                }, 1);
            console.log(this.completed);
        },
        statusTrue() {
            this.completed = document.querySelector('#statusTrueBtn').value
            setTimeout(() => {
                    this.$router.go()
                }, 1);
            console.log(this.completed);
        },
        statusFalse() {
            this.completed = document.querySelector('#statusFalseBtn').value
            setTimeout(() => {
                    this.$router.go()
                }, 1);
            console.log(this.completed);
        },
        prefix() {
            if (this.userDetailId != this.data[this.propsPageId].userId) {
                this.$router.push({path:'/'+ this.userDetailId + '/' + this.prevPage,
                params : {
                    pageId : this.prevPage, userId : this.userDetailId
                }
                })
                setTimeout(() => {
                    this.$router.go()
                }, 1);
                } else {
                    alert('첫페이지입니다')
                }
            },
        unit() {
            if(this.userDetailId != this.data[this.propsPageId].userId) {
                alert('마지막페이지입니다')
            }   else {
                this.$router.push({path:'/'+ this.userDetailId + '/' + this.nextPage,
                params : {
                    pageId : this.nextPage, userId : this.userDetailId
                }
                })
            setTimeout(() => {
                this.$router.go()
            }, 1);
            }
        }
    }


    }

    


</script>

<style>

</style>