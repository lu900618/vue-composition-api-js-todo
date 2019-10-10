<template>
  <div class="status">
    <label for="all">
      All
      <input type="radio" name="status" id="all" value="all" v-model="status" />
    </label>
    <label for="completed">
      Completed
      <input type="radio" name="status" id="completed" value="completed" v-model="status" />
    </label>
    <label for="uncompleted">
      Uncompleted
      <input
        type="radio"
        name="status"
        id="uncompleted"
        value="uncompleted"
        v-model="status"
      />
    </label>
  </div>
</template>

<script>
import { reactive, watch, toRefs } from '@vue/composition-api'
export default {
  setup (props, { emit }) {
    const data = reactive({ status: 'all' })

    // watch([() => data.a, () => data.b, () => data.c], ([val1, val2, val3]) => { console.log('conditions changed，do search', val1, val2, val3) })
    watch(() => data.status, val => {
      emit('change', val)
    })

    return {
      ...toRefs(data)
    }
  }
  // data () {
  //   return {
  //     status: 'all'
  //   }
  // },
  // watch: {
  //   status (val) {
  //     this.$emit('change', val)
  //   }
  // }
}
</script>

<style lang="less" scoped>
.status {
  padding: 10px 0;
  display: flex;
  justify-content: space-between;
}
</style>
