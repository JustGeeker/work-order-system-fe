/*
 * @Author: Skye Young 
 * @Date: 2019-10-28 19:47:31 
 * @Last Modified by: Skye Young
 * @Last Modified time: 2019-11-28 22:15:55
 */

<template>
  <main class="user">
    <user-card />
    <user-menu />
  </main>
</template>

<script lang="ts">
import Vue from "vue";
import UserCard from "@/components/User/Menu/UserCard.vue";
import UserMenu from "@/components/User/Menu/index.vue";

export default Vue.extend({
  name: "userIndex",
  components: {
    UserCard,
    UserMenu
  }
});
</script>

<style lang="scss" scoped>
@import "@/stylesheet/default.scss";

.user {
  display: flex;
  align-items: center;
  justify-content: space-between;

  height: 90vh;
  width: 85vw;
}

@include screen($larger) {
  .user {
    width: $static-card-width * 4;
  }
}
</style>