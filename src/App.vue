<template>
  <div>
    <!-- ToDoListを使用する -->
    <!-- <ToDoList />
    <CounterParent /> -->
    <Axsios-test />
  </div>
</template>

<script>
import ToDoList from './components/ToDoList.vue'
import CounterParent from './components/CounterParent.vue'
import AxsiosTest from './components/AxsiosTest.vue'
export default {
  name: 'App',
  components: {
    ToDoList,
    CounterParent,
    AxsiosTest
  }
}
</script>
