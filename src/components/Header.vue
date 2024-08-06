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
          v-model="searchQuery"
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
  }
}
</script>

<style lang="less">
.header-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid rgba(204, 204, 230, 0.7); /* 更柔和的边框颜色 */
  border-radius: 10px; /* 边框圆滑度 */
  padding: 10px 0; /* 添加内边距，使元素看起来更大更圆滑 */

  .header-left {
    display: flex;
    align-items: center;

    div {
      width: 50px;
      height: 50px;
      border-radius: 50%; /* 圆形按钮 */
      background: #9999E6;
      font-size: 30px;
      text-align: center;
      margin-right: 15px;
      color: #fff; /* 字体颜色更可爱 */
    }
  }

  .header-right {
    .headerAllSelect {
      background: #46e6e0;
      border-radius: 20px; /* 更圆滑的按钮 */
      font-size: 16px; /* 字体大小调整，使字体更可爱 */
      font-family: '宋体', sans-serif;
    }

    .headerAdd {
      background: #70B870;
      border-radius: 20px; /* 更圆滑的按钮 */
      font-size: 16px;
      font-family: sans-serif;
    }

    .headerDelete {
      background: #C43F38; /* 删除按钮颜色保持不变 */
      border-radius: 20px; /* 更圆滑的按钮 */
      margin-left: 10px;
      font-size: 16px;
      font-family: sans-serif;

    }
  }

  .search-input {
    padding: 0.5px;
    border: 0.5px solid rgba(204, 204, 230, 0.7); /* 更柔和的边框颜色 */
    border-radius: 4px; /* 边框圆滑度 */
    margin-left: 10px;
    color: rgba(0, 0, 0, 0.98); /* 输入框文字颜色 */
    font-size: 16px;
    font-family:  sans-serif;
  }
}
</style>
