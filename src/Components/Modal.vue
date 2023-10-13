<template>
  <div class="modal">
    <header>
      <span>{{ title }}</span>
      <button 
        class="close"
        @click="$emit('close')"
      >
        <svg fill="none" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16">
          <path d="M3.414 2 2 3.414 6.586 8 2 12.586 3.414 14 8 9.414 12.585 14 14 12.585 9.414 8 14 3.415 12.585 2 8 6.586 3.414 2Z" fill="currentColor"/>
        </svg>
      </button>
    </header>
    <div class="modal-body">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
    props: ['title']
}
</script>

<style lang="scss">
.modal {
  width: 100%;
  max-height: 100%;
  display: flex;
  flex-direction: column;
  background-color: var(--background1);
  overflow: hidden;
  border-radius: 4px;
  box-shadow: 0px 40px 80px -40px #000, 
              0px 24px 40px -24px rgba(0, 0, 0, 0.25), 
              0px 16px 24px -16px rgba(0, 0, 0, 0.25), 
              0px 4px 8px -4px rgba(0, 0, 0, 0.25);  

  header{
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: space-between;
    padding: 8px;
    line-height: 1.1;
    font-weight: 600;
    font-size: var(--font-size-large);
    color: var(--text1);
    border-bottom: 1px solid var(--border1);

    .close {
      padding: 0;
      margin: 0;
      background-color: transparent;
      border: none;
      outline: none;
      cursor: pointer;
      color: var(--text3);

      svg {
        width: 16px;
        height: 16px;
      }

      &:hover {
        color: var(--text1);
      }
    }
  }
}
</style>