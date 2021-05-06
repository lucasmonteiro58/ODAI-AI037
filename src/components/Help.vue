<template>
  <section class="container">
    <div class="backdrop"></div>
    <div class="image" :class="[helps[index].image, helps[index].class]"></div>
    <div
      class="text-ballon"
      :class="helps[index].class"
      v-html="textBallon"
    ></div>
    <div class="button-section" :class="helps[index].class">
      <div class="top">
        <button v-if="index !== 0" class="btn continuar" @click="voltarClick">
          <div class="text">Voltar</div>
        </button>
        <button class="btn continuar" @click="avancarClick">
          <div class="text">{{ nxtBtn }}</div>
        </button>
      </div>
      <button class="btn close btn-fechar" @click.prevent="clickClose">
        <div class="text">Fechar</div>
      </button>
    </div>
  </section>
</template>
<script>
import { helps } from '../consts/help'
export default {
  props: {
    index: {
      type: Number,
      required: true
    },
    isInitial: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      helps
    }
  },
  computed: {
    nxtBtn() {
      if (this.index === 2) return 'Vamos lá'
      else return 'Avançar'
    },
    textBallon() {
      if (this.isInitial) return this.helps[this.index].text
      else return this.helps[this.index].textAfter
    }
  },
  mounted() {},
  methods: {
    voltarClick() {
      this.$emit('voltar')
    },
    clickClose() {
      this.$emit('close')
    },
    avancarClick() {
      this.$emit('avancar')
    }
  }
}
</script>
<style lang="scss" scoped>
.container {
  @include flex-center;
  flex-direction: column;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 10;

  .backdrop {
    position: absolute;
    background-color: #000000a1;
    width: 100%;
    height: 100%;
  }

  .image {
    position: absolute;

    &.class-help0 {
      left: 40px;
      top: 140px;
    }

    &.class-help1 {
      left: 40px;
      top: 21px;
    }

    &.class-help2 {
      left: 53px;
      top: 124px;
    }
  }

  .text-ballon {
    position: absolute;
    text-align: center;
    //background-color: rgba(0, 0, 255, 0.151);
    line-height: 18px;
    font-size: 15px;
    font-weight: 500;

    .text-bold {
      font-weight: 1000;
      color: #000;
    }

    &.class-help0 {
      width: 334px;
      left: 343px;
      top: 182px;
    }

    &.class-help1 {
      width: 403px;
      left: 354px;
      top: 86px;
    }

    &.class-help2 {
      width: 361px;
      left: 471px;
      top: 250px;
    }
  }

  .button-section {
    position: absolute;
    display: flex;
    align-items: center;
    justify-items: center;
    flex-direction: column;
    gap: 10px;

    &.class-help0 {
      left: 460px;
      top: 310px;
    }

    &.class-help1 {
      left: 475px;
      top: 229px;
    }

    &.class-help2 {
      left: 579px;
      top: 402px;
    }
    .top {
      display: flex;
      gap: 12px;
    }
  }
}
</style>
