<template>
  <div v-show="showed" class="pop-up">
    <div class="backdrop"></div>
    <div class="content">
      <div class="top">
        <button class="btn primary" @click.prevent="clickInicio">
          <div class="icon iconeinicio"></div>
          <div class="text">Início</div>
        </button>
      </div>
      <div class="bottom">
        <button class="btn primary" @click.prevent="clickSom">
          <div class="icon" :class="soundClass"></div>
          <div class="text">Som</div>
        </button>
        <button class="btn primary" @click.prevent="clickCreditos">
          <div class="icon iconecreditos"></div>
          <div class="text text-creditos">Créditos</div>
        </button>
      </div>
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
    },
    soundState: {
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
  computed: {
    soundClass() {
      if (this.soundState) return 'ico-sound'
      else return 'ico-sound-off'
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
    clickSom() {
      this.$emit('som')
    },
    clickCreditos() {
      this.$emit('creditos')
    },
    clickInicio() {
      this.$emit('inicio')
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
    background-color: #00000090;
    width: 100%;
    height: 100%;
  }

  .content {
    position: relative;
    width: 220px;
    height: 215px;
    background: #ede0b0;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.25);
    border-radius: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 20px;

    .btn-fechar {
      position: absolute;
      bottom: -37px;
    }

    .bottom {
      display: flex;
      gap: 20px;

      .btn {
        .text-creditos {
          font-size: 10px;
        }
      }
    }
  }
}
</style>
