<template>
  <div class="content">
    <TodoItem
        v-for="(item, index) in filteredTodoList"
        :key="item.id"
        :item="item"
        :index="index"
        :handleSelect="handleSelect"
        :handleDelItem="handleDelItem"
        :handleBlur="handleBlur"
    />
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
  components: {
    TodoItem
  },
  props: {
    filteredTodoList: {
      type: Array,
      required: true
    },
    handleSelect: {
      type: Function,
      required: true
    },
    handleDelItem: {
      type: Function,
      required: true
    },
    handleBlur: {
      type: Function,
      required: true
    }
  }
}
</script>

<style lang="less">
.content {
  margin-top: 20px;
  height: 450px;
  overflow-y: scroll;
}
</style>
