<template>
  <header
    class="preview"
    :style="bgStyle"
  >
    <div class="box-wrapper">
      <div class="box" :style="boxStyle"></div>
    </div>
    <slot></slot>
  </header>
</template>

<script>
export default {
  props: ['bgColor', 'boxColor', 'shadow'],
  computed: {
    background() {
      const { r, g, b } = this.bgColor;
      return `rgba(${r},${g},${b},1)`;
    },
    foreground() {
      const { r, g, b } = this.boxColor;
      return `rgba(${r},${g},${b},1)`;
    },
    bgStyle() {
      return `background-color: ${this.background}`
    },
    boxStyle() {
      return `background-color: ${this.foreground}; box-shadow: ${this.shadow};`
    }
  },
}
</script>

<style lang="scss">
.preview {
  width: 100%;
  height: 262px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;

  .box-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    overflow: hidden;
    width: 100%;
    height: 100%;
    padding-bottom: 32px;
  }

  .box {
    width: 124px;
    height: 124px;
    border-radius: 8px;
  }
}
</style>
