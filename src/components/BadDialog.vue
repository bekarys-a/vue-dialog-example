<template>
  <el-dialog
    v-model="dialogVisible"
    title="Опрос"
    width="300px"
    :before-close="close"
  >
    <el-row style="margin-bottom: 8px">
      <el-input v-model="model" />
    </el-row>
    <el-row justify="end">
      <el-button @click="close">Закрыть</el-button>
      <el-button
        type="primary"
        @click="accept"
      >
        Принят
      </el-button>
    </el-row>
  </el-dialog>
</template>

<script setup lang="ts">
import { ref, watch} from 'vue'
import { ElRow, ElButton, ElDialog } from 'element-plus'

const model = ref<string>()
const dialogVisible = defineModel()
const props = defineProps<{
  text: string
}>()

watch(
  () => props.text,
  (value) => (model.value = value),
  {
    immediate: true,
  }
)

const emit = defineEmits<{
  change: [text: string]
}>()

function accept() {
  emit('change', model.value)
  dialogVisible.value = false
}

function close() {
  dialogVisible.value = false
}
</script>
