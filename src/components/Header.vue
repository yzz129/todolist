<template>
  <div class="header-box">
    <div class="header-left">
      <div>+</div>
      <h2>Todo List</h2>
    </div>
    <div class="header-right">
      <input
          type="text"
          class="search-input"
          placeholder="搜索..."
          v-model="localSearchQuery"
          @input="updateSearchQuery(localSearchQuery)"
      />
      <button class="headerAllSelect" @click="handleAllSelect">全选</button>
      <button class="headerAdd" @click="handleAdd">添加</button>
      <button class="headerDelete" @click="handleDeleteSelected">删除已选</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    searchQuery: {
      type: String,
      required: true
    },
    handleAllSelect: {
      type: Function,
      required: true
    },
    handleAdd: {
      type: Function,
      required: true
    },
    handleDeleteSelected: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      localSearchQuery: this.searchQuery
    };
  },
  watch: {
    searchQuery(newVal) {
      this.localSearchQuery = newVal;
    }
  },
  methods: {
    updateSearchQuery(newQuery) {
      this.$emit('update:searchQuery', newQuery);
    }
  }
}
</script>

<style lang="less">
.header-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: #ccc 1px solid;

  .header-left {
    display: flex;
    align-items: center;

    div {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      background: #9999E6;
      font-size: 30px;
      text-align: center;
      margin-right: 15px;
    }
  }

  .header-right {
    .headerAllSelect {
      background: #27b6c8;
      border-radius: 20px; /* 更圆滑的按钮 */
      font-family: sans-serif;
    }

    .headerAdd {
      background: #70B870;
      border-radius: 20px; /* 更圆滑的按钮 */
      font-family: sans-serif;
    }

    .headerDelete {
      background: #C43F38; // 设置删除按钮的样式
      margin-left: 10px;
      border-radius: 20px; /* 更圆滑的按钮 */
      font-family: sans-serif;
    }
  }
}

.search-input {
  padding: 1px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-left: 10px;
  color: #000; // 输入框文字颜色
  font-family: sans-serif;
}
</style>
