<template>
    姓名:
    <inline-edit v-model:value="value">
    </inline-edit>
</template>


<script setup lang="ts">
import {defineComponent, ref} from 'vue';
import InlineEdit from './components/InlineEdit.vue';

const value = ref('Ruyut');


defineComponent({
  components: {
    'inline-edit': InlineEdit
  },
});

</script>