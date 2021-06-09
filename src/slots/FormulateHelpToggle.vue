<template>
  <div>
    <div
      :class="['help-toggle', {_open: isOpen}]"
      @click="isOpen = !isOpen"
    >
      <transition
        name="fade-toggle"
        mode="out-in"
      >
        <span :key="isOpen">{{ isOpen ? 'Скрыть' : 'Подробнее' }}</span>
      </transition>
    </div>
    <transition name="fade">
      <div
        v-if="context.helpToggle && isOpen"
        :id="`${context.id}-help-toggle`"
        :class="context.classes.helpToggle"
        v-text="context.helpToggle"
      />
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    context: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      isOpen: false
    }
  }
}
</script>
<style lang="scss">
.help-toggle {
  display: inline-flex;
  align-items: center;
  justify-content: flex-start;
  color: #6B7182;
  cursor: pointer;

  &:not(:last-child) {
    margin-bottom: 4px;
  }

  &::before {
    display: block;
    width: 0;
    height: 0;
    margin-right: 6px;
    border-top: 6px solid #6B7182;
    border-right: 6px solid transparent;
    border-left: 6px solid transparent;
    border-bottom: none;
    background-color: transparent;
    transition-duration: 300ms;
    content: '';
  }

  &._open::before {
    transform: rotate(180deg);
  }
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 300ms;
}
.fade-toggle-enter-active, .fade-toggle-leave-active {
  transition: opacity 150ms;
}
.fade-enter, .fade-leave-to,
.fade-toggle-enter, .fade-toggle-leave-to  {
  opacity: 0;
}
</style>
