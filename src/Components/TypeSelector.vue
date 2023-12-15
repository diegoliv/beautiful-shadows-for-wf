<template>
  <nav class="shadow-type-selector">
    <div class="shadow-type-buttons">
      <input type="radio" value="box-shadow" v-model="value" id="shadow-type-box" tabindex="0">
      <label for="shadow-type-box" class="shadow-type-button">Box Shadow</label>
      <input type="radio" value="text-shadow" v-model="value" id="shadow-type-text" tabindex="0">
      <label for="shadow-type-text" class="shadow-type-button">Text Shadow</label>
    </div>
  </nav>
</template>

<script>
export default {
  name: "TypeSelector",
  props: ['modelValue'],
  emits: ['update:modelValue'],
  computed: {
    value: {
      get() {
        return this.modelValue
      },
      set(val) {
        this.$emit('update:modelValue', val)
      }
    }
  }
}
</script>

<style lang="scss">
.shadow-type-selector {
  position: absolute;
  top: 4px;
  left: 0;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;

  .shadow-type-buttons {
    display: flex;
    font-size: var(--font-size-small);
    border-radius: var(--border-radius);
    background-color: var(--background1);
    background-image: var(--actionSecondaryBackground);
    box-shadow: var(--boxShadows-action-secondary);
    padding: 1px;
    height: 24px;
  }

  .shadow-type-button {
    display: flex;
    width: 96px;
    align-items: center;
    justify-content: center;
    background-color: transparent;
    border: none;
    color: var(--actionSecondaryText);
    line-height: 24px;
    border-radius: var(--border-radius);
    cursor: pointer;


    &:hover {
      color: var(--text1);
    }
  }

  input[type="radio"] {
    opacity: 0;
    position: absolute;
    

    &:checked + label {
      background-color: var(--background1);
      box-shadow: var(--input-inner-shadow);
    }
    &:focus + label {
      outline: 1px solid var(--blueBorder);
    }
  }  
}
</style>