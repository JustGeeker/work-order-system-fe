/*
 * @Author: Skye Young 
 * @Date: 2019-10-28 19:47:39 
 * @Last Modified by: Skye Young
 * @Last Modified time: 2019-12-19 17:27:53
 */

<template>
  <main-card>
    <template v-slot:header>
      <back-link @click="$router.push({ name: 'index'})"></back-link>
      <vertical-divider isTransparent="true"></vertical-divider>
      <el-button
        type="text"
        @click="$router.push({ name: 'userInfoProfile'})"
        :disabled="btnIsDisabled"
      >个人资料</el-button>
      <vertical-divider></vertical-divider>
      <el-button
        type="text"
        @click="$router.push({ name: 'userInfoPassword'})"
        :disabled="!btnIsDisabled"
      >修改密码</el-button>
    </template>
    <router-view></router-view>
  </main-card>
</template>

<script lang="ts">
import Vue from "vue";
import MainCard from "@/components/User/Etc/MainCard.vue";
import BackLink from "@/components/Etc/BackLink.vue";
import VerticalDivider from "@/components/Etc/VerticalDivider.vue";

export default Vue.extend({
  components: {
    MainCard,
    BackLink,
    VerticalDivider
  },
  computed: {
    btnIsDisabled() {
      if (this.$route.name === "userInfoProfile") {
        return true;
      } else {
        return false;
      }
    }
  }
});
</script>