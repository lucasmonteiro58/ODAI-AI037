<template>
  <div v-show="showed" class="pop-up">
    <div class="backdrop" @click.prevent="clickClose"></div>
    <div class="content">
      <div class="list-creditos">
        <div class="title">Créditos</div>
        <b>IMAGENS RASTERIZADAS:</b>
        <p class="last">Ilustração dos 7 erros por Beatriz Mayum</p>
        <b>IMAGENS VETORIAIS: </b>
        <p>Magnifying Glass por Karl Schaeffler do Noun Project</p>
        <p>Sound por Adrien Coquet do Noun Project</p>
        <p>Home por icongeek do Noun Project</p>
        <p>
          Female Detective With Magnifying Glass Background por brgfx do
          Freepik.com
        </p>
        <p>Magnifying Glass Icon Business por rawpixel.com do Freepik.com</p>
        <p class="last">
          Various Round Floral Laurel Frames Set Logo por pch.vector do
          Freepik.com
        </p>
        <b>SONS:</b>
        <p>User interface menu sounds.wav por oussamaben do Freesound.org</p>
        <p>mouth pops por chestnutjam do Freesound.org</p>
        <p>Click.m4a por Splatez07 do Freesound.org</p>
        <p class="last">WinBanjo.wav por Fupicat do Freesound.org</p>
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
    width: 630px;
    height: 423px;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.25);
    border-radius: 20px;
    background: #ede0b0;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    .list-creditos {
      width: 90%;
      text-align: center;
      line-height: 18px;

      .title {
        font-size: 24px;
        margin-bottom: 30px;
      }

      .last {
        margin-bottom: 20px;
      }
      p {
        text-transform: initial;
      }
    }
    .btn-fechar {
      position: absolute;
      bottom: -37px;
    }
  }
}
</style>
