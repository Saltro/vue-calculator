<template>
  <div id="container">
    <span id="result">{{ result }}</span>
    <button id="ac">AC</button>
    <button id="not">±</button>
    <button id="percent">%</button>
    <button id="division">÷</button>
    <button id="seven">7</button>
    <button id="eight">8</button>
    <button id="nine">9</button>
    <button id="multiply">×</button>
    <button id="four">4</button>
    <button id="five">5</button>
    <button id="six">6</button>
    <button id="minus">-</button>
    <button id="one">1</button>
    <button id="two">2</button>
    <button id="three">3</button>
    <button id="plus">+</button>
    <button id="zero">0</button>
    <button id="dot">.</button>
    <button id="equal">=</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "@vue/runtime-core";

export default defineComponent({
  setup () {
    const result = ref<string>('0')
    
    return {
      result
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
    color: #646464;
    grid-area: res;
    font-size: 64px;
    text-align: right;
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