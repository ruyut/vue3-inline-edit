<template>
  <input v-if="editMode"
         ref="inputRef"
         type="text" v-model="inputValue" @blur="save" @keyup.enter="save"/>
  <span v-else @click="toggleEdit" class="editable-content">{{ value }}</span>
</template>

<script setup lang="ts">
import {nextTick, ref} from 'vue';

const editMode = ref(false);
const inputRef = ref(null);
const inputValue = ref('');

const props = defineProps({
  value: null as any,
})

/**
 * 切換編輯模式
 */
function toggleEdit() {
  inputValue.value = props.value;
  editMode.value = true;

  nextTick(() => {
    inputRef.value.focus(); // 取得焦點
  });
}

const emits = defineEmits(['update:value']);

/**
 * 離開編輯模式，儲存資料並發送資料修改通知
 */
function save() {
  emits('update:value', inputValue.value); // 發送資料修改通知
  editMode.value = false;
}

</script>

<style scoped>
.editable-content {
  display: inline-block; /* 內容為空時也維持矩形 */
  min-width: 50px; /* 限制最小寬度 */
  min-height: 10px; /* 限制最小高度 */
  padding: 2px 5px; /* 增加內距 */
  border: 1px solid transparent; /* 透明邊框 */
  border-radius: 4px; /* 設定圓角 */
  background-color: #f9f9f9; /* 設定背景色 */
  vertical-align: baseline; /* 對齊基線 */
}

.editable-content:hover {
  background-color: #e6e6e6; /* 滑鼠懸停時改變背景色 */
  cursor: pointer; /* 改變滑鼠游標為點擊狀態 */
}
</style>