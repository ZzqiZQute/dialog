<script lang="ts" setup>
  withDefaults(defineProps<{
    // 接受v-model属性
    modelValue: boolean;
    // 对话框标题
    title: string;
    // 对话框内容
    content: string;
    // 是否展示关闭按钮 (?: 表示这是一个可选的属性，用withDefault设置默认值）
    showCloseButton?: boolean
  }>(), {
    // 设置默认值为true
    showCloseButton: true,
  })
  const emit = defineEmits<{
    // 发射v-model变化
    (event: 'update:modelValue', value: boolean): void;
  }>();
  const handleClose = () => {
    // 用函数的形式传给v-on 调用
    emit('update:modelValue', false);
  };
</script>

<template>
  <!-- 用v-if控制元素展示 -->
  <div v-if="modelValue" class="dialog-container">
    <div class="dialog">
      <!-- 用v-if展示关闭弹窗按钮 -->
      <div v-if="showCloseButton" class="close">
        <!-- 模版中使用emit需要用 $emit -->
        <div @click="$emit('update:modelValue', false)">关闭1</div>
        <div @click="handleClose">关闭2</div>
      </div>
      <div class="dialog-title">
        {{ title }}
      </div>
      <div class="dialog-content">
        {{ content }}
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  // 首先创建一个全屏的容器，把对话框放在他里面
  .dialog-container {
    // 使用fixed布局
    position: fixed;
    // 宽度是100%
    width: 100%;
    // 高度是100%
    height: 100%;
    // z轴索引设置大一点，让他盖住下面的内容
    z-index: 999;
    // 设置flex布局，然后居中
    display: flex;
    // 水平居中
    justify-content: center;
    // 垂直居中
    align-items: center;
    // 设置背景是灰色的，突出对话框  设置透明度 否则后面的就看不到了
    background: rgba(#000, 0.1);
    // 里面写对话框的本体
    .dialog {
      // 设置宽度
      width: 500px;
      // 设置高度
      height: 300px;
      // 设置背景
      background: #fff;
      // 内边距
      padding: 20px;
      // 圆角
      border-radius: 16px;
      // 设置position为relative, 使关闭的按钮用absolute控制位置
      position: relative;
      .close {
        position: absolute;
        // 设置在右上角
        right: 20px;
        top: 20px;
        > div { // 子元素选择器  #id选择器  .类选择器 tag标签选择器
          // 里面两个按钮都设置是光标是小手
          cursor: pointer;
        }
      }
      .dialog-title {
        font-size: 24px;
        color: #222;
      }
      .dialog-content {
        font-size: 16px;
        margin-top: 20px;
        color: #333;
      }
    }
  }
</style>