<template>
  <div class="todoListBox">
    <Header
        :searchQuery="searchQuery"
        :handleAllSelect="handleAllSelect"
        :handleAdd="handleAdd"
        :handleDeleteSelected="handleDeleteSelected"
    />
    <TodoList
        :filteredTodoList="filteredTodoList"
        :handleSelect="handleSelect"
        :handleDelItem="handleDelItem"
        :handleBlur="handleBlur"
    />
  </div>
</template>

<script>
import dayjs from "dayjs";
import Header from './components/Header.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    Header,
    TodoList
  },
  data() {
    return {
      todoList: [],
      searchQuery: '' // 添加搜索查询
    }
  },
  created() {
    let getList = JSON.parse(window.localStorage.getItem("listTodo1"))
    if (getList === null) {
      this.todoList = [{
        id: this.randomID(),
        text: "请点击上方的添加按钮添加事件",
        isSelected: false,
        time: dayjs(new Date).format('YY-MM-DD HH:mm')
      }]
    } else {
      this.todoList = getList
    }
  },
  computed: {
    filteredTodoList() {
      return this.todoList.filter(item =>
          item.text.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }
  },
  methods: {
    // 添加功能
    handleAdd() {
      this.todoList.unshift({
        id: this.randomID(),
        isCheck: false, // 是否选中
        text: "", // input 框内容
        time: dayjs(new Date).format("YY-MM-DD HH:mm"), // 时间
      })

      const inputLength = this.todoList.length - 1
      // 获取焦点
      this.$nextTick(() => {
        this.$refs.inputBox[inputLength].focus()
      })
    },
    // 删除功能
    handleDelItem(index, id) {
      if (this.todoList[index].id === id) {
        this.todoList.splice(index, 1)
        this.storage()
      }
    },
    // 选中功能
    handleSelect(index, id) {
      if (this.todoList[index].id === id) {
        this.todoList[index].isCheck = !this.todoList[index].isCheck
        this.storage()
      }
    },
    // 全选功能
    handleAllSelect() {
      this.todoList.forEach(item => {
        item.isCheck = !item.isCheck
        this.storage()
      })
    },
    // 一键删除功能
    handleDeleteSelected() {
      this.todoList = this.todoList.filter(item => !item.isCheck);
      this.storage();
    },
    // 判断是否输入完成
    handleBlur() {
      this.storage()
    },
    // 生成随机ID
    randomID() {
      return Number(Math.random().toString().substr(2, 0) + Date.now()).toString(10)
    },
    // 本地存储
    storage() {
      window.localStorage.setItem('listTodo1', JSON.stringify(this.todoList))
    }
  }
}
</script>

<style lang="less">
.todoListBox {
  width: 800px;
  height: 600px;
  background: #3C3E4F;
  border-radius: 10px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px;
  box-sizing: border-box;
  color: #fff;
}
</style>