<template>
  <!-- <div>
    <span>count is {{ count }}</span>
    <span>plusOne is {{ plusOne }}</span>
    <button @click="increment">count++</button>
  </div>-->
  <div class="main">
    <Inputer @submit="submit" />
    <Status @change="onStatusChanged" />
    <TodoList :list="onShowList" @toggle="toggleStatus" @delete="onItemDelete" />
  </div>
</template>

<script>
// import { ref, computed, watch, onMounted } from '@vue/composition-api'
import { reactive, computed, toRefs } from '@vue/composition-api'
import Inputer from './components/Inputer'
import TodoList from './components/TodoList'
import Status from './components/Status'

export default {
  components: {
    Inputer,
    TodoList,
    Status
  },
  setup () {
    const data = reactive({
      todoList: [],
      showingStatus: 'all',
      onShowList: computed(() => {
        if (data.showingStatus === 'all') {
          return data.todoList
        } else if (data.showingStatus === 'completed') {
          return data.todoList.filter(({ completed }) => completed)
        } else if (data.showingStatus === 'uncompleted') {
          return data.todoList.filter(({ completed }) => !completed)
        }
      })
    })

    function submit (content) {
      data.todoList.push({
        completed: false,
        content,
        id: parseInt(Math.random(0, 1) * 100000)
      })
    }
    function onStatusChanged (status) {
      data.showingStatus = status
    }
    function toggleStatus ({ isChecked, id }) {
      data.todoList.forEach(item => {
        if (item.id === id) {
          item.completed = isChecked
        }
      })
    }
    function onItemDelete (id) {
      let index = 0
      data.todoList.forEach((item, i) => {
        if (item.id === id) {
          index = i
        }
      })
      data.todoList.splice(index, 1)
    }

    return {
      ...toRefs(data),
      submit,
      onStatusChanged,
      toggleStatus,
      onItemDelete
    }
    // // reactive state
    // const count = ref(0)
    // // computed state
    // const plusOne = computed(() => count.value + 1)
    // // method
    // const increment = () => { count.value++ }
    // // watch
    // watch(() => count.value * 2, val => {
    //   console.log(`count * 2 is ${val}`)
    // })
    // // lifecycle
    // onMounted(() => {
    //   console.log(`mounted`)
    // })
    // // expose bindings on render context
    // return {
    //   count,
    //   plusOne,
    //   increment
    // }
  }
}
</script>
