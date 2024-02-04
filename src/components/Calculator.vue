<template>
    <div>
        <h1>Hello Avd</h1>
        <div class="calculator">
            <div class="display">{{result || "0"}}</div>
            <div class="btn" @click="clear">C</div>
            <div class="btn" @click="changeSign">+/-</div>
            <div class="btn " @click="percent">%</div>
            <div class="btn operator" @click="divide">/</div>
            <div class="btn" @click="append(7)">7</div>
            <div class="btn" @click="append(8)">8</div>
            <div class="btn" @click="append(9)">9</div>
            <div class="btn operator" @click="multiple">*</div>
            <div class="btn" @click="append(4)">4</div>
            <div class="btn" @click="append(5)">5</div>
            <div class="btn" @click="append(6)">6</div>
            <div class="btn operator" @click="minus">-</div>
            <div class="btn" @click="append(1)">1</div>
            <div class="btn" @click="append(2)">2</div>
            <div class="btn" @click="append(3)">3</div>
            <div class="btn operator" @click="add">+</div>
            <div class="btn zero" @click="append(0)">0</div>
            <div class="btn" @click="decimalPoint">.</div>
            <div class="btn operator" @click="submit">=</div>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            result : "",
            operator : null,
            previous : null,
            clickedOperator : false

        }
    },
    methods: {
        clear() {
            this.result = "";
        },
        changeSign () {
            this.result =this.result.charAt(0) === '-' ?
            this.result.slice(1) : `-${this.result}`;
        },
        percent() {
            this.result = `${parseFloat(this.result) / 100}`;
        },
        append(num) {
            if (this.clickedOperator) {
                this.result = '';
                this.clickedOperator = false
            }
            this.result = `${this.result}${num}`
        },
        decimalPoint() {
            if (this.result.indexOf('.') === -1) {
                this.append('.')
            }
        },
        setPrevious() {
            this.previous = this.result;
            this.clickedOperator = true;
        },
        divide () {
            this.operator = (a, b) => a / b;
            this.setPrevious();
        },
        multiple () {
            this.operator = (a, b) => a * b;
            this.setPrevious();
        },
        minus () {
            this.operator = (a, b) => a - b;
            this.setPrevious();
        },
        add () {
            this.operator = (a, b) => a + b;
            this.setPrevious();
        },
        submit () {
            this.result = `${this.operator(parseFloat(this.result),parseFloat(this.previous))}`;
            this.previous = null;
        }
    },
}
</script>

<style>
.calculator {
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px ,auto);
    text-align: center;
}
.display {
    grid-column: 1 / 5;
    background-color: black;
    color: white ;
}
.zero {
    grid-column: 1/3;
}
.btn {
    background-color: #eee;
    border: 1px solid black;
}
.operator {
    background-color: orange;
    color: white;
}
</style>