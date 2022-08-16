<template>

   <div> 
    
  <input type="text" v-model="searchKeyword" />

    <div v-if="userList === null" class="loader">
        <img width="70" src="https://mir-s3-cdn-cf.behance.net/project_modules/disp/04de2e31234507.564a1d23645bf.gif" />
        <h4>데이터를 불러오는 중입니다.</h4>
    </div>
    <div v-else-if="userList.length < 1" class="loader">
        <h4>
            <img width="40" src="https://cdn-icons-png.flaticon.com/512/179/179386.png?w=360" />
            유저가 발견되지 않았습니다.
        </h4>
    </div>
    <div v-else v-for="(char, idx) in charGroup" :key="idx">
        <h4 class="group-title">{{ char }}</h4>
        <div v-for="(user, idx) in filteredUserList" :key="idx">

            <div class="user-item" v-if="user.name.substring(0,1) === char">
                <h4><router-link :to="{name : 'board', params:
                {
                    id : user.id,
                }}">{{user.name}}</router-link></h4>
            </div>

        </div>
    </div>
</div>

</template>

<script>

export default {

    //다른 컴포넌트로부터 속성(attribute)을 통해 전달받을 수 있는 인자를 지정
    props: {

    },
    //이 컴포넌트에서 사용할 다른 컴포넌트 "등록"
    //다만, 컴포넌트는 등록하기전에 "선언" 해야한다 (import)
    components: {

    },
    // 이 컴포넌트 안에서 사용할 함수 선언
    methods : {

    },
    // 이 컴포넌트 안에서 사용할 변수 선언
    data() {
        return {
            userList: this.$userList,
            charGroup : [],
            searchKeyword : '',
        }
    },
    // 이 컴포넌트의 로드가 완료되면 해야 할 동작
    mounted() {
        this.bVariable = 40;

        this.filteredUserList.filter(
            (user) => {
                let groupKey = user.name.substring(0,1);

                if(this.charGroup.indexOf(groupKey) === -1){
                    this.charGroup.push(groupKey);
                }
    
                console.log(this.charGroup);
                console.log(user.name.substring(0,1));
                return true;
            }
        );
    },
    computed: {
        filteredUserList(){
            return this.userList.filter(
                //여기서부터
                (user) => {
                    return user.name.toLowerCase().includes(
                            this.searchKeyword.toLowerCase()
                        );
                }
                //여기까지 함수입니다 :)
            );
        },
        calcResult(){
            let result = this.aVariable + this.bVariable * this.aVariable;
            return result;
        }
    }
}
</script>

<style>
.group-title{
    background:#eee;
    padding:5px;
    margin-bottom:10px;
}
.user-item{
    padding:20px;
    margin:10px;
    border-radius:10px;
    border:1px solid #eee;
}
</style>