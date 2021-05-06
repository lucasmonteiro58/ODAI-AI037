<template>
  <div v-show="showed" class="pop-up">
    <div class="backdrop" @click.prevent="clickClose"></div>
    <div class="content">
      <button class="btn close btn-fechar" @click.prevent="clickClose">
        <div class="text">Fechar</div>
      </button>
    </div>
  </div>
</template>

<script>
import { fadeOut, fromTop } from '../assets/animate'
export default {
  name: 'PopUpOpcoes',
  props: {
    isShowed: {
      type: Boolean,
      required: false,
      default: true
    }
  },
  data() {
    return {
      showed: false
    }
  },
  watch: {
    isShowed(val, old) {
      if (!old && val) {
        this.showed = true
        this.showAnimation()
      } else if (old && !val) {
        this.showed = false
      }
    }
  },
  mounted() {
    if (this.isShowed) this.showed = true
    this.showAnimation()
  },
  beforeDestroy() {
    fadeOut(this.$el)
  },
  methods: {
    showAnimation() {
      fromTop(this.$el.lastChild)
    },
    clickClose() {
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
    background-color: #00000070;
    width: 100%;
    height: 100%;
  }

  .content {
    width: 400px;
    height: 300px;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.25);
    border-radius: 20px;
    background: #ede0b0;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    .btn-fechar {
      position: absolute;
      bottom: -37px;
    }
  }
}
</style>
