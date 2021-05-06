<template>
  <div class="pop-up">
    <div class="backdrop"></div>
    <div class="content">
      <div class="congrats-image"></div>
      <div class="text-ballon">
        <div class="title">MUITO BEM!!!</div>
        <p>
          Você investigou como um verdadeiro detetive, e livrou a família de
          muitos perigos de acidente! Agora devemos sempre estar de olhos bem
          abertos para estes perigos em qualquer lugar! Aqui está sua lupa de
          ouro, detetive, você merece!
        </p>
      </div>
      <div class="buttons-section">
        <button class="btn continuar" @click="voltarClick">
          <div class="text">voltar</div>
        </button>
        <button class="btn continuar" @click="reiniciarClick">
          <div class="text">reiniciar</div>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PopUp',
  methods: {
    voltarClick() {
      this.$emit('voltar')
    },
    reiniciarClick() {
      this.$emit('reiniciar')
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
    background-color: #0000009f;
    width: 100%;
    height: 100%;
  }

  .content {
    position: absolute;

    .buttons-section {
      position: absolute;
      bottom: 13px;
      left: 334px;
      display: flex;
      grid-gap: 10px;
      gap: 15px;
    }

    .text-ballon {
      width: 431px;
      text-align: center;
      position: absolute;
      top: 30px;
      left: 151px;
      .title {
        color: #000;
        font-size: 17px;
      }
      p {
        font-family: MplusRegular;
        font-size: 15px;
      }
    }
  }
}
</style>
