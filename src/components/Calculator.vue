
<template>
  <div class="calculator ">
    <div class="current">{{ current || "0" }}</div>
    <div @click="append('7')" class="btn grid-line">7</div>
    <div @click="append('8')" class="btn grid-line">8</div>
    <div @click="append('9')" class="btn grid-line">9</div>
    <div @click="add" class="btn grid-line symbol">+</div>
    <div @click="append('4')" class="btn grid-line">4</div>
    <div @click="append('5')" class="btn grid-line">5</div>
    <div @click="append('6')" class="btn grid-line">6</div>
    <div @click="minus" class="btn grid-line symbol">-</div>
    <div @click="append('1')" class="btn grid-line">1</div>
    <div @click="append('2')" class="btn grid-line">2</div>
    <div @click="append('3')" class="btn grid-line">3</div>
    <div @click="multiply" class="btn grid-line symbol">*</div>
    <div @click="clear" class="btn grid-line symbol">C</div>
    <div @click="append('0')" class="btn grid-line">0</div>
    <div @click="equals" class="btn grid-line symbol">=</div>
    <div @click="divide" class="btn grid-line symbol">/</div>
  </div>
</template>

<script>
export default {
    data() {
        return{
            previous: null,    
            current: '',
            operator: null,
            operartorClicked: false,
        }
    },
    methods: {
        clear() {
            this.current = ''
        },
        append(number) {
            if (this.operartorClicked) {
                this.current = '';
                this.operartorClicked = false;
            }
            this.current = `${this.current}${number}`;
        },
        setPrevious() {
            this.previous = this.current;
            this.operartorClicked = true;
        },
        add() {
            this.operator = (a, b) => a + b;
            this.setPrevious();
        },
        minus() {
            this.operator = (a, b) => a - b;
            this.setPrevious();
        },
        multiply() {
            this.operator = (a, b) => a * b;
            this.setPrevious();
        },
        divide() {
            this.operator = (a, b) => a / b;
            this.setPrevious();
        },
        equals() {
            this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`;
            this.previous = null;
        }
    },
}
</script>


<style>
.calculator {
    margin: 10rem auto;
    width: 300px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: minmax(50px, auto);
}

.current {
    font-size: 40px;
    text-align: right;
    grid-column: 1 / 5;
    background-color: black;
    color: white;
}

.btn {
    color: black;
    font-size: 32px;
    text-align: center;
    background-color: cornflowerblue;
}

.symbol {
    color:black;
    background-color: brown;
}

.grid-line {
    border: 1px solid black;
}
</style>
