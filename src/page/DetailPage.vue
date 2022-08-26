<template>
  <div>

        <user-item :type="2"  :propsUserId="userId" :propsCompleted="userBoardList" :propsPageId="pageId"/>
  </div>
</template>

<script>
import userItem from '../components/userItem.vue'
export default {
     data() {
        return {
            userId : this.$route.params.userId,
            pageId : this.$route.params.pageId,
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