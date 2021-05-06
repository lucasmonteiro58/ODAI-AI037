<template>
  <div v-show="showed" class="pop-up">
    <div class="backdrop"></div>
    <div class="content">
      <div class="left-content">
        <div class="title">{{ erro.title }}</div>
        <div class="text">
          {{ erro.text }}
        </div>
      </div>
      <div class="right-content">
        <div class="image" :class="erro.image"></div>
        <button class="btn continuar" @click="closeErros">
          <div class="text">Continuar</div>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { fadeOut, fromTop } from '../assets/animate'
export default {
  name: 'PopUpErros',
  props: {
    isShowed: {
      type: Boolean,
      required: false,
      default: true
    },
    erro: {
      type: Object,
      requeried: true,
      default: () => {
        return {}
      }
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
    closeErros() {
      this.$emit('close')
      this.showed = false
    },
    showAnimation() {
      fromTop(this.$el.lastChild)
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
    width: 462px;
    height: 225px;
    background: #ede0b0;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.25);
    border-radius: 20px;
    display: flex;

    .left-content {
      padding: 20px 0px 20px 20px;
      .title {
        font-size: 20px;
        line-height: 39px;
        text-align: center;
        color: #000000;
        margin-top: -10px;
      }
      .text {
        font-size: 16px;
        font-weight: 500;
        line-height: 20px;
      }
    }
    .right-content {
      padding: 20px;
      .image {
        margin-bottom: 10px;
      }
    }
  }
}
</style>
