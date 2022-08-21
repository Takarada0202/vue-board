<template>
  <div>

        <user-item :type="1"  :propsUserId="this.userId" :propsCompleted="this.userBoardList"/>
  </div>
</template>

<script>
import userItem from '../components/userItem.vue'
export default {
     data() {
        return {
            userId : this.$route.params.id,
            userBoardList : null,
        }
    },
    components : {
        userItem,
    }
}


</script>

<style>

</style>