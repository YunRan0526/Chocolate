<template>
  <el-upload
    class="avatar-uploader"
    :show-file-list="false"
    :on-change="getFileUrl"
    :auto-upload="false"
  >
    <img v-if="imageUrl" :src="imageUrl" class="avatar" />
    <el-icon v-else class="avatar-uploader-icon"><Plus /></el-icon>
  </el-upload>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { Plus } from "@element-plus/icons-vue";
const emit = defineEmits(["getFileUrl"]);
const imageUrl = ref<string>("");
const getFileUrl = (uploadFile: { raw: Blob }): void => {
  const url = URL.createObjectURL(uploadFile.raw);
  imageUrl.value = url;
  emit("getFileUrl", url);
};
</script>

<style scoped>
.avatar-uploader .avatar {
  width: 178px;
  height: 178px;
  display: block;
}
</style>

<style>
.avatar-uploader .el-upload {
  border: 1px dashed var(--el-border-color);
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  transition: var(--el-transition-duration-fast);
}

.avatar-uploader .el-upload:hover {
  border-color: var(--el-color-primary);
}

.el-icon.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 178px;
  height: 178px;
  text-align: center;
}
</style>
