/*
 * @Author: Skye Young 
 * @Date: 2019-10-28 19:49:36 
 * @Last Modified by:   Skye Young 
 * @Last Modified time: 2019-10-28 19:49:36 
 */

<template>
  <div class="bruce flex-ct-x">
    <ul class="reflect-loading">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({});
</script>

<style lang="scss" scoped>
$count: 10;
$color: $purple $blue;

.reflect-loading {
  display: flex;
  height: 100px;
  -webkit-box-reflect: below 0 linear-gradient(rgba(#fff, 0), rgba(#fff, 0.7));
  li {
    width: 20px;
    @for $i from 0 to $count {
      $args: append($color, $i * 100% / ($count - 1));
      &:nth-child(#{$i + 1}) {
        background-color: mix($args...);
        animation: rotate 3s cubic-bezier(0.81, 0.04, 0.4, 0.7) infinite;
        animation-delay: $i * 50ms;
      }
    }
  }
}
@keyframes rotate {
  0% {
    transform: rotate(-0.5turn) rotateX(-1turn);
  }
  75%,
  100% {
    transform: none;
  }
}
</style>