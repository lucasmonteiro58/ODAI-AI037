<template>
  <div class="pop-up">
    <div class="backdrop"></div>
    <div class="content">
      <div class="congrats-image"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PopUp',
  methods: {
    closeCreditos() {
      this.$emit('close')
    }
  }
}
</script>

<style lang="scss" scoped>
.title-popup {
  font-size: 32px;
}
.pop-up {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 500;
  display: flex;
  align-items: center;
  justify-content: center;

  .backdrop {
    position: absolute;
    background-color: #00000031;
    width: 100%;
    height: 100%;
  }
}
</style>
