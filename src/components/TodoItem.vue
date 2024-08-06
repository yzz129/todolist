<template>
  <div class="content-item">
    <div class="content-left" @click="handleSelect(index, item.id)">
      <span :style="item.isCheck ? 'opacity: 1' : 'opacity: 0'"></span>
    </div>
    <input
        type="text"
        class="content-input"
        v-model="item.text"
        :disabled="item.isCheck"
        :class="item.isCheck ? 'line-through' : ''"
        @blur="handleBlur"
        ref="inputBox"
    />
    <div class="content-right">
      <p>{{ item.time }}</p>
      <button @click="handleDelItem(index, item.id)">删除</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
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
.content-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #6B6F7D;
  border-radius: 8px;
  padding: 10px 20px;
  box-sizing: border-box;
  margin-top: 20px;

  .content-left {
    width: 30px;
    height: 30px;
    border: 1px solid #ccc;
    border-radius: 50%;
    position: relative;

    span {
      display: inline-block;
      width: 20px;
      height: 20px;
      background: #9999E6;
      border-radius: 50%;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }

  .content-input {
    flex: 1;
    margin: 0 10px;
    outline: none;
    background: transparent;
    border: none;
    border-bottom: 1px solid #ccc;
    padding: 5px 10px;
    color: #fff;
  }

  .line-through {
    color: rgba(255, 255, 255, 0.3); // 文字颜色
    text-decoration: line-through rgba(255, 255, 255, 0.8); // 横线颜色
  }

  .content-right {
    display: flex;
    align-items: center;

    button {
      background: #C43F38;
    }
  }
}
</style>