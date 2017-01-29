<template>
    <div class="counter">
        <div>
          <button class="counter__modify" @click="increment">+</button>
          <span class="counter__modify"> {{finalValue}} </span>
          <button class="counter__modify" @click="decrement">-</button>
        </div>
        <div>
          <button class="counter__alert" @click="get">GET</button>
          <button class="counter__alert" @click="reset">RESET</button>
          <button class="counter__alert" @click="set">SET</button>
          <input class="counter__alert" type="text" v-model="val"/>
          <button class="counter__alert" @click="$emit('remove')">DELETE</button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'counter',
  data () {
    return {
        value: this.initValue,
        size: this.initSize,
        val: ''
      }
  },
  props: {
    initValue: {
      type: Number,
      default: 0
    },
    initSize: {
      type: Number,
      default: 3
    }
  },
  methods: {
    increment() {
      this.value++;
    },
    decrement() {
      this.value--;
    },
    get() {
      alert(this.value);
    },
    reset() {
      this.value = 0;
    },
    set() {
      this.value = this.val;
      this.val = '';
    }
  },
  watch: {
    value(newVal) {
      if(newVal > this.maxSize)
         this.value = this.maxSize;
      if(newVal < 0)
         this.value = 0;
    }
  },
  computed: {
    maxSize() {
    let maxSize = 0;
    for(let i = 0; i < this.size; i++) {
      maxSize += (Math.pow(10, i) * 9)
    }
    return maxSize;
    },
    finalValue() {
        const length = String(this.value).length;
        const zeros = this.size - length;
        let finalValue = "";
        for (var i = 0; i < zeros; i++) {
            finalValue += "0";
        }
        finalValue += this.value;
        return finalValue;
      }
  },
}
</script>

<style>
html {
   font-size: 16px;
}

.body {
    background-color: #808080;
}

.counter {
    text-align: center;
}

.counter_add {
    height: 35px;
    font-size: 1.5rem;
    float: right;
}

.counter__modify {
    font-size: 2rem;
    font-weight: bold;
    cursor: pointer;
    transition: color 0.5s linear;
}

.counter__modify:hover {
    color: rgba(0, 0, 0, .3);
}

span.counter__modify {
    margin: 0 3px 0 3px;
}

button, input {
    background-image: -webkit-linear-gradient(top, #f4f1ee, #fff);
    background-image: linear-gradient(top, #f4f1ee, #fff);
    border-radius: 20%;
    box-shadow: 0px 8px 10px 0px rgba(0, 0, 0, .3), inset 0px 4px 1px 1px white, inset 0px -3px 1px 1px rgba(204,198,197,.5);
    -webkit-transition: all .1s linear;
    transition: all .1s linear;
}

button.counter__modify {
    height: 50px;
    margin: 0 0px 15px 0;
    width: 50px;
}

button.counter__alert {
    height: 50px;
    margin: 0 15px 50px 0;
    width: auto;
}

input.counter__alert {
    height: 45px;
    width: 100px;
    margin: 0 15px 50px 0;
}

.counter__alert {
    font-size: 1.25rem;
    font-weight: bold;
    cursor: pointer;
    transition: color 0.5s linear;
}

.counter__alert:hover {
    color: rgba(0, 0, 0, .3);
}

input[type=number]::-webkit-inner-spin-button,
input[type=number]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

input[type=number] {
    -moz-appearance: textfield;
}
</style>
