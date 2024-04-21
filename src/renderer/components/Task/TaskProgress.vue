<template>
  <el-progress
    class="mo-task-progress"
    :percentage="percent"
    :show-text="true"
    :color="color"
>
  </el-progress>
</template>

<script>
  import { TASK_STATUS } from '@shared/constants'
  import { calcProgress } from '@shared/utils'
  import colors from '@shared/colors'

  export default {
    name: 'mo-task-progress',
    props: {
      total: {
        type: Number
      },
      completed: {
        type: Number
      },
      status: {
        type: String,
        default: TASK_STATUS.ACTIVE
      }
    },
    computed: {
      isActive () {
        return this.status === TASK_STATUS.ACTIVE
      },
      percent () {
        return calcProgress(this.total, this.completed)
      },
      color () {
        return colors[this.status]
      }
    }
  }
</script>

<style>
  .mo-task-progress .el-progress-bar {
    width: calc(100% - 10px);
  }
</style>
