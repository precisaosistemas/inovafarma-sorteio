<template>
  <el-row type="flex" justify="center">
    <el-col>
      <div class="sorteio">
        <div class="bloco-conteudo">
          <lottie
            :options="defaultOptions" 
            :height="240" 
            :width="400" 
            @animCreated="boxAnimation"
            class="caixa-animacao"/>
          <div 
            class="numero-sorteio"
            :class="{ active: firstClick }">
            {{ displayNumber }}</div>
        </div>

        <h1 class="titulo">{{ message }}</h1>


        <div class="numero-escolha">
          <el-input-number v-model="number1" :min="1"></el-input-number>
          <el-input-number v-model="number2" :min="number1"></el-input-number>
        </div>

        <div class="botao-sorteio">
          <el-button type="primary" @click="rollPrize" round><i class="el-icon-refresh"></i> Sortear número</el-button>
          <lottie
            :options="defaultOptions2" 
            :height="180" 
            :width="180"
            @animCreated="bubbleAnimation"
            class="botao-animacao"/>
        </div>
        
      </div>
    </el-col>
  </el-row>
</template>

<script>
  import _ from 'lodash'
  import Lottie from 'vue-lottie'
  import * as boxAnimation from '@/assets/boxAnimation.json'
  import * as bubbleAnimation from '@/assets/bubble.json'

  export default {
    name: 'landing-page',
    components: {
      'lottie': Lottie
    },
    data () {
      return {
        message: 'INOVAFARMA Sorteio',
        number1: null,
        number2: 50,
        number: 0,
        displayNumber: 0,
        interval: false,
        firstClick: false,
        defaultOptions2: {
          animationData: bubbleAnimation,
          loop: false,
          autoplay: false
        },
        defaultOptions: {
          animationData: boxAnimation,
          loop: false,
          autoplay: true
        },
        animationSpeed: 0.7
      }
    },
    methods: {
      boxAnimation: function (anim) {
        this.boxAnim = anim
        this.boxAnim.setSpeed(this.animationSpeed)
      },
      bubbleAnimation: function (anim) {
        this.bubbleAnim = anim
        this.bubbleAnim.setSpeed(this.animationSpeed)
      },
      rollPrize () {
        this.firstClick = true
        this.boxAnim.stop()
        this.boxAnim.play()
        this.bubbleAnim.stop()
        this.bubbleAnim.play()
        this.number = _.random(this.number1, this.number2)
      }
    },
    watch: {
      number () {
        clearInterval(this.interval)
        if (this.number === this.displayNumber) {
          return
        }
        this.interval = window.setInterval(function() { // eslint-disable-line
          if (this.displayNumber !== this.number) {
            let change = (this.number - this.displayNumber) / 200
            change = change >= 0 ? Math.ceil(change) : Math.floor(change)
            this.displayNumber = this.displayNumber + change
          } else {
            clearInterval(this.interval)
          }
        }.bind(this), 40)
      }
    }
  }
</script>

<style lang="scss">
.el-row {
  height: 100%;
  align-items: center;
  justify-content: center;
  text-align: center;
}
.el-tag {
  font-size: 40px;
  height: auto;
  line-height: auto;
}
.titulo{
  margin-top: 0;
  color: #5A6279;
}
.botao-sorteio {
  position: relative;
  margin-top: 26px;
  .el-button {
    position: relative;
    z-index: 2;
  }
  .botao-animacao {
    pointer-events: none;
    position: absolute;
    top: -70px;
    left: 0;
    right: 0;
    margin: auto;
    z-index: 1;
  }
}
.bloco-conteudo {
  position: relative;
  .caixa-animacao {
    position: relative;
    z-index: 2;
  }
  .numero-sorteio {
    left:0;right:0;top:4px;bottom:0;
    position: absolute;
    margin: 2px auto 20px auto;
    background-color: #FF6661;
    font-size: 46px;
    font-weight: bold;
    color: #fff;
    width: 80px;
    height: 80px;
    line-height: 80px;
    border-radius: 50%;
    text-align: center;
    opacity: 0;
    transform: translateY(40px);
    transition: all .5s ease .6s;
    &.active {
      opacity: 1;
      transform: translateY(0px);
    }
  }
}
</style>
