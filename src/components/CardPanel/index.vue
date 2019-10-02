<template>
  <transition name="slide-fade">
    <div class="card__panel" v-if="showPanel">
      <button class="card__panel-close" @click="$emit('close')" >X</button>
      <h1>Добавьте свою гипотезу</h1>
    </div>
  </transition>
</template>

<script>
  export default {
    name: 'CardPanel',
    props: ['showPanel']

  }
</script>

<style lang="scss" scoped>

.card__panel {
  position: absolute;
  top: 0;
  right: 0;
  width: 447px;
  height: 100%;
  background: #FFFFFF;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.25);
  &-close {
    background: transparent;
    border: none;
    cursor: pointer;
    position: absolute;
    top: 5px;
    right: 5px;
  }
}
    .slide-fade-enter-active {
      transition: all .3s ease;
    }
    .slide-fade-leave-active {
      transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .slide-fade-enter, .slide-fade-leave-to
    {
      transform: translateX(10px);
      opacity: 0;
    }
</style>
