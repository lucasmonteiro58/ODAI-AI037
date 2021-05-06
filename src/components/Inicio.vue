<template>
  <section class="container bg-inicio">
    <button class="btn iniciar btn-inicio" @click="iniciarClick">
      <div class="text">iniciar</div>
    </button>
  </section>
</template>
<script>
export default {
  methods: {
    iniciarClick() {
      this.$emit('iniciar')
    }
  }
}
</script>
<style lang="scss" scoped>
.container {
  @include flex-center;
  flex-direction: column;
  z-index: 3;
}

.btn-inicio {
  position: absolute;
  left: 522px;
  top: 607px;
}
</style>
