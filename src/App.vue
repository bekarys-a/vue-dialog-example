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
    <h1>{{ text }}</h1>
    <div>
      <el-button
        type="primary"
        @click="editGood"
      >
        промис
      </el-button>
      <el-button
        type="primary"
        @click="badVisible = true"
      >
        стандартный
      </el-button>
    </div>
  </div>
  <GoodDialog ref="GoodDialogRef" />
  <BadDialog
    v-model="badVisible"
    :text="text"
    @change="(value) => (text = value)"
  />
</template>

<script setup lang="ts">
import GoodDialog from '@/components/GoodDialog.vue'
import BadDialog from '@/components/BadDialog.vue'
import { ElMessage, ElButton } from 'element-plus'
import { ref, useTemplateRef } from 'vue'

const text = ref<string>('hello')

const badVisible = ref(false)

type GoodDialogType = InstanceType<typeof GoodDialog>
const GoodDialogRef = useTemplateRef<GoodDialogType>('GoodDialogRef')

async function editGood() {
  try {
    text.value = await GoodDialogRef.value!.open(text.value)
    ElMessage({
      message: 'успешно изменено',
      type: 'success',
    })
  } catch {
    ElMessage({
      message: 'не сохранено',
      type: 'error',
    })
  }
}
</script>
