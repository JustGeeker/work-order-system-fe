/*
 * @Author: Skye Young
 * @Date: 2019-11-30 18:19:10
 * @Last Modified by: Skye Young
 * @Last Modified time: 2019-12-01 13:57:48
 */


<template>
  <span class="upload-btn">
    <el-button type="primary" @click="showUploadDialog">
      <slot></slot>
    </el-button>
    <el-dialog :visible.sync="isVisible" :close-on-click-modal="false" append-to-body>
      <div slot="title">上传文件</div>
      <div class="upload-field">
        <upload-file ref="uploadField" :custom-api="api"></upload-file>
      </div>
    </el-dialog>
  </span>
</template>

<script lang="ts">
import Vue from "vue";
import UploadFile from "@/components/Etc/UploadFile.vue";
import { AxiosResponse } from "axios/";

export default Vue.extend({
  props: ["api"],
  components: {
    UploadFile
  },
  data() {
    return {
      isDisable: false,
      isVisible: false
    };
  },
  computed: {
    btnText() {
      if (this.isDisable) {
        return "文件上传结束";
      } else {
        return "文件上传中...";
      }
    }
  },
  methods: {
    showUploadDialog() {
      this.isVisible = !this.isVisible;
    }
  }
});
</script>

<style lang="scss" scoped>
.sightless {
  opacity: 0;
  pointer-events: none;
}
</style>

<style lang="scss">
.el-dialog {
  width: 30vw;
}

.upload-btn {
  margin-inline-start: 15px;
}

.upload-field {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
