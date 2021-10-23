<template>
  <div id="container">
    <div id="result" ref="resultBox">
      <span ref="resultNum">{{ result }}</span>
    </div>
    <button id="ac" @click="result = '0'">AC</button>
    <button id="not" @click="reverse">±</button>
    <button id="percent" @click="percent">%</button>
    <button id="division" @click="add('÷')">÷</button>
    <button id="seven" @click="add('7')">7</button>
    <button id="eight" @click="add('8')">8</button>
    <button id="nine" @click="add('9')">9</button>
    <button id="multiply" @click="add('×')">×</button>
    <button id="four" @click="add('4')">4</button>
    <button id="five" @click="add('5')">5</button>
    <button id="six" @click="add('6')">6</button>
    <button id="minus" @click="add('-')">-</button>
    <button id="one" @click="add('1')">1</button>
    <button id="two" @click="add('2')">2</button>
    <button id="three" @click="add('3')">3</button>
    <button id="plus" @click="add('+')">+</button>
    <button id="zero" @click="add('0')">0</button>
    <button id="dot" @click="add('.')">.</button>
    <button id="equal" @click="calcResult">=</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, computed } from "@vue/runtime-core";

export default defineComponent({
  setup () {
    const resultTemp = ref<string>('0')
    let numberLength = 0

    const result = computed({
      get: () => {
        // console.log('get', resultTemp.value)
        return resultTemp.value
      },
      set: (val) => {
        // console.log('set', val)
        if (val.length > numberLength) {
          val = val.slice(0, numberLength)
        }
        resultTemp.value = val
      }
    })

    const resultBox = ref<Element>(document.createElement('a'))
    const resultNum = ref<Element>(document.createElement('a'))

    onMounted(() => {
      numberLength = resultBox.value.clientWidth / resultNum.value.clientWidth
    })

    const isOperation = (symbol: string) => ['+', '-', '÷', '×', '.'].includes(symbol)
    const isLastOperation = () => isOperation(getLastSymbol())
    const isZero = () => result.value === '0'
    const getLastSymbol = () => result.value.charAt(result.value.length - 1)
    const popResult = () => result.value = result.value.slice(0, result.value.length - 1)

    const add = (symbol: string) => {
      if (result.value === 'ERROR') {
        result.value = ''
      }
      if (isOperation(symbol)) {
        if (isLastOperation()) {
          switch (symbol) {
            case '+':
            case '÷':
            case '×':
              popResult()
              break
            case '-':
              if (getLastSymbol() === '+' || getLastSymbol() === '-') {
                popResult()
              }
              break
            case '.':
              symbol = ''
              break
          }
        } else {
          switch (symbol) {
            case '-':
              if (isZero()) {
                result.value = ''
              }
              break
          }
        }
      } else {
        if (isZero()) {
          result.value = ''
        }
      }
      result.value += symbol
    }

    const calcResult = () => {
      if (isLastOperation()) {
        popResult()
      }
      result.value = result.value.replaceAll('×', '*')
      result.value = result.value.replaceAll('÷', '/')
      // console.log(result.value)
      try {
        result.value = eval(result.value).toString()
      } catch (e) {
        if (e instanceof SyntaxError) {
          result.value = 'ERROR'
        }
      }
    }

    const reverse = () => {
      calcResult()
      if (result.value !== 'ERROR' && result.value !== '0') {
        if (result.value[0] === '-') {
          result.value = result.value.slice(1)
        } else {
          result.value = '-' + result.value
        }
      }
    }

    const percent = () => {
      calcResult()
      if (result.value !== 'ERROR') {
        result.value = (+result.value / 100).toString()
      }
    }
    
    return {
      result,
      add,
      calcResult,
      reverse,
      percent,
      resultBox,
      resultNum
    }
  }
})

function popResult() {
throw new Error("Function not implemented.");
}
</script>

<style lang="scss" scoped>
#container {
  border-radius: 30px;
  box-sizing: border-box;
  display: grid;
  grid-template-rows: repeat(6, 90px);
  grid-template-columns: repeat(4, 90px);
  grid-template-areas: 'res res res res'
                       'ac notbtn per div'
                       'seven eight nine mul'
                       'four five six minus'
                       'one two three plus'
                       'zero zero dot equal';
  gap: 15px;
  padding: 50px 40px 40px;
  background-color: #EAEAEA;
  box-shadow: 5px 5px 15px rgba($color: #000000, $alpha: 0.1),
              -5px -5px 15px rgba($color: #FFFFFF, $alpha: 0.6);
  
  #result {
    grid-area: res;
    overflow: hidden;
    span {
      font-size: 64px;
      text-align: right;
      color: #646464;
      float: right;
    }
  }
  
  button {
    font-size: 36px;
    color: #8B8B8B;
    background-color: #EAEAEA;
    border: none;
    border-radius: 50%;
    box-shadow: 3px 3px 8px rgba($color: #000000, $alpha: 0.05),
              -3px -3px 8px rgba($color: #FFFFFF, $alpha: 0.3),
              inset 4px 4px 20px rgba($color: #000000, $alpha: 0.04),
              inset -4px -4px 20px rgba($color: #FFFFFF, $alpha: 0.5);
  }

  button:active {
    box-shadow: inset 6px 6px 15px rgba($color: #000000, $alpha: 0.1),
                inset -6px -6px 15px rgba($color: #FFFFFF, $alpha: 0.4);
  }

  #ac {
    grid-area: ac;
  }

  #not {
    grid-area: notbtn;
  }

  #percent {
    grid-area: per;
  }
  
  #division {
    grid-area: div;
  }

  #seven {
    grid-area: seven;
  }

  #eight {
    grid-area: eight;
  }

  #nine {
    grid-area: nine;
  }

  #multiply {
    grid-area: mul;
  }

  #four {
    grid-area: four;
  }

  #five {
    grid-area: five;
  }

  #six {
    grid-area: six;
  }

  #minus {
    grid-area: minus;
  }

  #one {
    grid-area: one;
  }

  #two {
    grid-area: two;
  }

  #three {
    grid-area: three;
  }

  #plus {
    grid-area: plus;
  }

  #zero {
    grid-area: zero;
    border-radius: 60px;
  }

  #dot {
    grid-area: dot;
  }

  #equal {
    grid-area: equal;
  }
}

@media only screen and (max-width: 1023px) {
  #container {
    grid-template-rows: repeat(6, 60px);
    grid-template-columns: repeat(4, 60px);

    #result {
      span {
        font-size: 48px;
      }
    }

    button {
      font-size: 28px;
    }
  }
}
</style>