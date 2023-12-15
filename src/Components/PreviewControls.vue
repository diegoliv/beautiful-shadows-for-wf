<template>
  <div class="preview-footer">
    <button class="presets-trigger" @click="$emit('openpresets')">
      <svg fill="none" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16">
        <path
          fill="currentColor"
          d="M2 3.75h12v1.5H2zm0 3.5h12v1.5H2zm0 3.5h12v1.5H2z"
        />
      </svg>
      <span>Presets</span>
    </button>
    <div class="preview-colors">
      <div
        class="color foreground"
        :class="isForegroundPickerActive ? 'active' : ''"
        v-click-outside="onForegroundClickOutside"
      >
        <div class="color-picker-container" v-show="isForegroundPickerActive">
          <Chrome v-model="foreground" />
        </div>
        <button
          class="color-inner"
          :style="`background-color: ${this.foreground};`"
          @click="isForegroundPickerActive = !isForegroundPickerActive"
          tabindex="0"
        ></button>
      </div>
      <div
        class="color background"
        :class="isBackgroundPickerActive ? 'active' : ''"
        v-click-outside="onBackgroundClickOutside"
      >
        <div class="color-picker-container" v-show="isBackgroundPickerActive">
          <Chrome v-model="background" />
        </div>
        <button
          class="color-inner"
          :style="`background-color: ${this.background}`"
          @click="isBackgroundPickerActive = !isBackgroundPickerActive"
          tabindex="0"
        ></button>
      </div>
    </div>
  </div>
</template>

<script>
import { Chrome } from '@ckpack/vue-color'
import vClickOutside from 'click-outside-vue3'

export default {
  components: {
    Chrome
  },
  props: ['bgColor', 'boxColor'],
  directives: {
    clickOutside: vClickOutside.directive
  },
  data () {
    return {
      isForegroundPickerActive: false,
      isBackgroundPickerActive: false
    }
  },
  computed: {
    background: {
      get () {
        const { r, g, b } = this.bgColor
        return `rgba(${r},${g},${b},1)`
      },
      set (value) {
        this.$emit('setbgcolor', value.rgba)
      }
    },
    foreground: {
      get () {
        const { r, g, b } = this.boxColor
        return `rgba(${r},${g},${b},1)`
      },
      set (value) {
        this.$emit('setboxcolor', value.rgba)
      }
    },
  },
  methods: {
    onForegroundClickOutside (event) {
      this.isForegroundPickerActive = false
    },
    onBackgroundClickOutside (event) {
      this.isBackgroundPickerActive = false
    }
  }
}
</script>

<style lang="scss">
.preview-footer {
  position: absolute;
  top: 214px;
  left: 0;
  width: 100%;
  padding: 0 16px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;

  .color-picker-container {
    position: absolute;
    bottom: auto;
    top: 0;
    right: 100%;
    z-index: 11;
    padding-right: 4px;
  }    

  .preview-colors {
    display: flex;
  }

  .color-inner {
    width: 32px;
    height: 32px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    box-shadow: 0px 8px 8px -4px rgba(0, 0, 0, 0.25),
      0px 4px 4px -2px rgba(0, 0, 0, 0.25),
      inset 0 0 0 1px rgba(255, 255, 255, 1);
    border-radius: 32px;
    cursor: pointer;

    &:focus {
      outline: 1px solid var(--blueBorder);
    }
  }

  .color {
    position: relative;
    z-index: 2;
    + .color {
      margin-left: -16px;
      z-index: 1;
    }
    &.active {
      z-index: 20;
    }
  }
}

.presets-trigger {
  position: relative;
  display: flex;
  align-items: center;
  padding: 4px 8px 4px 4px;
  border: none;
  color: var(--actionSecondaryText);
  line-height: 1;
  font-size: var(--font-size-small);
  border-radius: var(--border-radius);
  background-color: var(--background1);
  background-image: var(--actionSecondaryBackground);
  box-shadow: var(--boxShadows-action-secondary);
  cursor: pointer;

  &:hover {
    background-image: var(--actionSecondaryBackgroundHover);
  }

  &:focus {
    outline: 1px solid var(--blueBorder);
  }

  svg {
    display: block;
    width: 16px;
    height: 16px;
    margin-right: 2px;
  }
}
</style>
