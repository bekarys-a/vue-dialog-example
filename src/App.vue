<template>
  <div
    style="
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
    "
  >
    <el-button
      type="primary"
      @click="edit"
    >
      пройти опрос
    </el-button>
    <h1>{{ result }}</h1>
  </div>
  <EditDialog ref="EditDialogRef" />
</template>

<script setup lang="ts">
import EditDialog from '@/components/EditDialog.vue'
import { ElMessage, ElButton } from 'element-plus'
import { ref, useTemplateRef } from 'vue'

type EditDialogType = InstanceType<typeof EditDialog>
const EditDialogRef = useTemplateRef<EditDialogType>('EditDialogRef')

const result = ref<string>()

async function edit() {
  try {
    result.value = await EditDialogRef.value!.open()
    ElMessage({
      message: 'успешно изменено',
      type: 'success',
    })
  } catch {
    result.value = undefined
    ElMessage({
      message: 'не сохранено',
      type: 'error',
    })
  }
}
</script>
