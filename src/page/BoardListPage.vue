<template>
  <div>
    {{userBoardList}}
    {{userId}}
  </div>
</template>

<script>
export default {
     data() {
        return {
            userId : this.$route.params.id,
            userBoardList : null,
        }
    },
    methods: {
        fetchData: function() {
            let self = this;

            this.$axios.get('https://jsonplaceholder.typicode.com/todos/?userId='+this.userId)
            .then(function(response) {
                // response
                if(response.status !== 200){
                    alert('통신에러!');
                    self.userBoardList = [];
                }else{
                    self.userBoardList = response.data;
                }
            })
            // .catch(function(error) {
            // console.log(error);
            // });
        },
    }
}
</script>

<style>

</style>