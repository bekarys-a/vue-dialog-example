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
import { ref } from 'vue'
import { ElRow, ElButton, ElDialog } from 'element-plus'

defineExpose({
  open,
})

const dialogVisible = ref(false)

type ResolveType = string
const model = ref<ResolveType>('')

let resolve: (value: ResolveType) => void
let reject: (value?: unknown) => void

function open(text: string) {
  model.value = text

  dialogVisible.value = true
  return new Promise<ResolveType>((ok, fail) => {
    resolve = ok
    reject = fail
  })
}

function accept() {
  dialogVisible.value = false
  resolve(model.value)
}

function close() {
  dialogVisible.value = false
  reject()
}
</script>
