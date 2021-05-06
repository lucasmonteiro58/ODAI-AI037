<template>
  <section class="container">
    <div class="hero">
      <div class="top-bar">
        <div v-if="showHelp" class="blocktop"></div>
        <button
          class="btn btn-help-opcoes primary z-index-opcoes"
          :class="'index-help' + indexHelp"
          @click.prevent="openPopUpOpcoes"
        >
          <div class="icon iconeopcoes"></div>
          <div class="text">Opções</div>
        </button>
        <button
          class="btn primary btn-help-opcoes"
          :class="'index-help' + indexHelp"
          @click.prevent="openHelp"
        >
          <div class="icon iconeajuda"></div>
          <div class="text">Ajuda</div>
        </button>
        <div class="rect-roxo">
          <div class="logo-jogo-top"></div>
        </div>
        <div
          class="rect-vermelho"
          :class="['color' + contErro, 'index-help' + indexHelp]"
        >
          {{ contErro + '/7' }}
        </div>
      </div>
      <div class="stage-images">
        <div class="imagemprincipal"></div>
        <div class="imagem-erro-erradas" @click.prevent="clickImageWrong"></div>
        <div class="container-erros">
          <div v-for="erro in erros" :key="erro.id">
            <div
              v-if="!erro.isFind"
              class="erro"
              :class="erro.name"
              @click="clickErro(erro)"
            ></div>
            <div v-else class="circle" :class="erro.circulo"></div>
          </div>
        </div>
      </div>
      <div class="legenda">
        VAMOS AJUDAR A DETETIVE A ENCONTRAR TODOS OS PERIGOS QUE ESTÃO
        ESPALHADOS PELA CASA!!
      </div>
    </div>
    <PopUpErros
      v-if="showPopUpErro"
      :is-showed="showPopUpErro"
      :erro="selectedErro"
      @close="closePopUpErro"
    ></PopUpErros>
    <PopUpCongrats
      v-if="showPopUpCongrats"
      @voltar="closePopUpCongrats"
      @reiniciar="reiniciarGame"
    ></PopUpCongrats>
    <PopUpOpcoes
      v-if="showPopUpOpcoes"
      :is-showed="showPopUpOpcoes"
      :sound-state="soundState"
      @close="closePopUpOpcoes"
      @inicio="goToIniciar"
      @som="toogleSound"
      @creditos="openCreditos"
    ></PopUpOpcoes>
    <PopUpCreditos
      v-if="showPopUpCreditos"
      :is-showed="showPopUpCreditos"
      @close="closePopUpCreditos"
    ></PopUpCreditos>
    <Help
      v-if="showHelp"
      :index="indexHelp"
      :is-initial="initialHelp"
      @close="closeHelp"
      @voltar="voltarHelp"
      @avancar="avancarHelp"
    ></Help>
    <Inicio v-if="showIniciar" @iniciar="iniciarClick"></Inicio>
  </section>
</template>
<script>
import PopUpCongrats from '../components/PopUpCongrats.vue'
import PopUpErros from '../components/PopUpErros.vue'
import Inicio from '../components/Inicio.vue'
import { erros } from '../consts/home'
import PopUpOpcoes from '../components/PopUpOpcoes.vue'
import Help from '../components/Help.vue'
import audios from '../mixins/audios'

export default {
  components: {
    PopUpErros,
    PopUpCongrats,
    Inicio,
    PopUpOpcoes,
    Help
  },
  mixins: [audios],
  data() {
    return {
      erros,
      selectedErro: erros[0],
      showPopUpErro: false,
      showPopUpCongrats: false,
      showPopUpOpcoes: false,
      showPopUpCreditos: false,
      showHelp: false,
      contErro: 0,
      indexHelp: 0,
      preventClick: true,
      showIniciar: true,
      initialHelp: true
    }
  },
  computed: {
    soundState() {
      return this.$store.state.soundState
    }
  },
  mounted() {
    this.$store.commit('changeBackground', 'bg-menu')
  },
  methods: {
    clickErro(el) {
      if (this.preventClick) {
        this.preventClick = false
        el.isFind = true
        if (this.soundState) this.audioCircle.play()

        setTimeout(() => {
          this.selectedErro = el
          this.showPopUpErro = true
          this.preventClick = true
          if (this.soundState) this.audioPopUp.play()
        }, 700)
      }
    },
    avancarHelp() {
      if (this.soundState) this.audioClick.play()
      if (this.indexHelp === 2) {
        this.showHelp = false
        this.indexHelp = 0
        this.initialHelp = false
      } else {
        this.indexHelp++
      }
    },
    clickImageWrong() {
      if (this.soundState) this.audioMissClick.play()
    },
    voltarHelp() {
      if (this.soundState) this.audioClick.play()
      this.indexHelp--
    },
    closeHelp() {
      if (this.soundState) this.audioClick.play()
      this.showHelp = false
      this.initialHelp = false
      this.indexHelp = 0
    },
    openHelp() {
      if (this.soundState) this.audioClick.play()
      this.showHelp = true
    },
    goToIniciar() {
      if (this.soundState) this.audioClick.play()
      this.showIniciar = true
      this.showPopUpOpcoes = false
      this.reiniciarGame()
    },
    iniciarClick() {
      if (this.soundState) this.audioClick.play()
      this.showIniciar = false
      this.showHelp = true
    },
    closePopUpErro() {
      if (this.soundState) this.audioClick.play()
      this.showPopUpErro = false
      this.contErro++
      if (this.contErro === 7) {
        setTimeout(() => {
          if (this.soundState) this.audioWin.play()
          this.showPopUpCongrats = true
        }, 500)
      }
    },
    closePopUpOpcoes() {
      if (this.soundState) this.audioClick.play()
      this.showPopUpOpcoes = false
    },
    openPopUpOpcoes() {
      if (this.soundState) this.audioPopUp.play()
      this.showPopUpOpcoes = true
    },
    toogleSound() {
      if (this.soundState) this.audioClick.play()
      this.$store.commit('changeSoundState', !this.soundState)
    },
    openCreditos() {
      if (this.soundState) this.audioPopUp.play()
      this.showPopUpCreditos = true
      this.showPopUpOpcoes = false
    },
    closePopUpCreditos() {
      if (this.soundState) this.audioClick.play()
      this.showPopUpCreditos = false
    },
    closePopUpCongrats() {
      if (this.soundState) this.audioClick.play()
      this.showPopUpCongrats = false
    },
    reiniciarGame() {
      this.showPopUpCongrats = false
      this.contErro = 0
      this.initialHelp = true
      this.erros = this.erros.map((el) => {
        el.isFind = false
        return el
      })
    }
  }
}
</script>
<style lang="scss" scoped>
.container {
  @include flex-center;
  flex-direction: column;
}

.imagem-erro-erradas {
  position: absolute;
  width: 463px;
  height: 579px;
  top: 0;
  left: 0;
  background-color: #ffffff00;
  cursor: pointer;
}

.blocktop {
  position: absolute;
  width: 300px;
  height: 100px;
  opacity: 0;
  top: 0px;
  left: 0px;
  z-index: 12;
}

.btn-help-opcoes {
  &.index-help2 {
    z-index: 11;
  }
}

.z-index-opcoes {
  z-index: 4;
}

.hero {
  position: absolute;
  margin-top: 40px;
  top: 0;
}

.top-bar {
  display: flex;
  justify-content: space-between;
  width: 944px;
}

.rect-roxo {
  width: 622px;
  height: 67px;
  border-radius: 17px;
  background-color: $roxo;
  position: relative;
  display: flex;
  justify-content: center;

  .logo-jogo-top {
    position: absolute;
    bottom: -5px;
  }
}

.legenda {
  color: #4e4e4e;
  width: 100%;
  text-align: center;
  margin-top: 8px;
}

.rect-vermelho {
  width: 141px;
  height: 67px;
  border-radius: 17px;
  font-size: 54px;
  padding-top: 6px;
  text-align: center;
  z-index: 2;

  &.index-help1 {
    z-index: 11;
  }

  &.color0 {
    background-color: #f86d66;
  }
  &.color1 {
    background-color: #f89e52;
  }
  &.color2 {
    background-color: #f7c044;
  }
  &.color3 {
    background-color: #f6e335;
  }
  &.color4 {
    background-color: #cee642;
  }
  &.color5 {
    background-color: #97e657;
  }
  &.color6 {
    background-color: #55e56f;
  }
  &.color7 {
    background-color: #55e5ae;
  }
}

.stage-images {
  margin-top: 32px;
  position: relative;
}

.iconeopcoes {
  margin-bottom: 5px;
}

.circle {
  position: absolute;

  &.c-escada {
    top: 153px;
    left: 272px;
  }

  &.c-agulhas {
    top: 330px;
    left: 322px;
  }

  &.c-tesoura {
    top: 305px;
    left: 378px;
  }

  &.c-tomada {
    top: 368px;
    left: 375px;
  }

  &.c-remedios {
    top: 364px;
    left: 183px;
  }

  &.c-balde {
    top: 396px;
    left: 129px;
  }

  &.c-mesa {
    top: 291px;
    left: 98px;
  }
}

.erro {
  position: absolute;
  cursor: pointer;
  background-color: blue;
  opacity: 0;
  z-index: 1;

  &.escada {
    width: 214px;
    height: 262px;
    top: 80px;
    left: 247px;
    clip-path: polygon(100% 0%, 100% 51%, 34% 100%, 0% 99%, 0 81%);
  }

  &.mesa {
    width: 100px;
    height: 83px;
    top: 278px;
    left: 105px;
  }

  &.balde {
    width: 41px;
    height: 58px;
    top: 405px;
    left: 155px;
  }

  &.remedios {
    width: 47px;
    height: 50px;
    top: 374px;
    left: 200px;
  }

  &.gaveta {
    width: 53px;
    height: 31px;
    top: 353px;
    left: 340px;
  }

  &.tesoura {
    width: 47px;
    height: 19px;
    top: 342px;
    left: 386px;
    clip-path: polygon(100% 0, 100% 100%, 26% 100%, 21% 45%, 0 45%, 0 0);
  }

  &.tomada {
    width: 30px;
    height: 31px;
    top: 391px;
    left: 402px;
  }
}
</style>
