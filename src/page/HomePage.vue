<template>
  <div>
    <h1>Home</h1>
        <user-item :type="0"/>
  </div>
</template>

<script>
import userItem from '../components/userItem.vue'
export default {
    components : {
        userItem,
    }
}
</script>

<style>

</style>