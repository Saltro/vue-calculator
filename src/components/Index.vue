<template>
  <div id="container">
    <div id="result" ref="resultBox">
      <span ref="resultNum">{{ result }}</span>
    </div>
    <button id="ac" @click="result = '0'">AC</button>
    <button id="not" @click="reverse">±</button>
    <button id="percent" @click="percent">%</button>
    <button id="division" @click="add('÷')">÷</button>
    <button id="seven" @click="add(7)">7</button>
    <button id="eight" @click="add(8)">8</button>
    <button id="nine" @click="add(9)">9</button>
    <button id="multiply" @click="add('×')">×</button>
    <button id="four" @click="add(4)">4</button>
    <button id="five" @click="add(5)">5</button>
    <button id="six" @click="add(6)">6</button>
    <button id="minus" @click="add('-')">-</button>
    <button id="one" @click="add(1)">1</button>
    <button id="two" @click="add(2)">2</button>
    <button id="three" @click="add(3)">3</button>
    <button id="plus" @click="add('+')">+</button>
    <button id="zero" @click="add(0)">0</button>
    <button id="dot" @click="add('.')">.</button>
    <button id="equal" @click="calcResult">=</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, getCurrentInstance, computed } from "@vue/runtime-core";

export default defineComponent({
  setup () {
    const resultTemp = ref<string>('0')
    let numberLength = 0

    const result = computed({
      get: () => {
        console.log('get', resultTemp.value)
        return resultTemp.value
      },
      set: (val) => {
        console.log('set', val)
        if (val.length > numberLength) {
          val = val.slice(0, numberLength)
        }
        resultTemp.value = val
      }
    })

    // const resultBox = ref(null)

    onMounted(() => {
      // console.log(getCurrentInstance()?.ctx.$refs.resultBox.clientWidth)
      // console.log(getCurrentInstance()?.ctx.$refs.resultNum.clientWidth)
      numberLength = getCurrentInstance()?.ctx.$refs.resultBox.clientWidth / getCurrentInstance()?.ctx.$refs.resultNum.clientWidth
      // console.log(numberLength)
    })

    const add = (symbol: number | string) => {
      if (result.value === 'ERROR') {
        result.value = ''
      }
      if (typeof symbol === 'number') {
        if (result.value === '0') {
          result.value = ''
        }
        symbol = symbol.toString()
      } else if (typeof symbol === 'string') {
        switch (symbol) {
          case '-':
            if (result.value === '0') {
              result.value = ''
            }
            break
        }
      }
      result.value += symbol
    }

    const calcResult = () => {
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
      percent
    }
  }
})
</script>

<style lang="scss" scoped>
#container {
  width: 90%;
  height: 90%;
  max-width: 500px;
  max-height: 750px;
  border-radius: 30px;
  box-sizing: border-box;
  display: grid;
  grid: repeat(6, 1fr) / repeat(4, 1fr);
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
</style>