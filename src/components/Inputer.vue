<template>
  <div class="inputer">
    <h2>TODO LIST</h2>
    <input type="text" v-model="todoContent" @keyup.enter="submit" />
  </div>
</template>

<script>
import { reactive, toRefs } from '@vue/composition-api'
export default {
  setup (props, { emit }) {
    const data = reactive({ todoContent: '' })
    function submit () {
      emit('submit', this.todoContent)
      data.todoContent = ''
    }
    return {
      ...toRefs(data),
      submit
    }
  }

}
</script>

<style lang="less" scoped>
.inputer {
  text-align: center;
  h2 {
    text-align: center;
  }
  input {
    border: 2px solid #333;
    width: 90vw;
    padding: 5px 10px;
    font-size: 24px;
  }
}
</style>
