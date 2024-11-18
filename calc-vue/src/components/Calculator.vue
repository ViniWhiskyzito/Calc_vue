<template>
    <div class="calculator">
        <CalculatorDisplay :value="displayValue" />
        
        <!-- Campos de entrada e select -->
        <div class="input-fields">
            <input 
                type="number" 
                v-model.number="num1" 
                placeholder="Primeiro número"
                class="number-input"
            >
            
            <select 
                v-model="operation" 
                class="operation-select"
            >
                <option value="add">+</option>
                <option value="subtract">-</option>
                <option value="multiply">×</option>
                <option value="divide">÷</option>
            </select>
            
            <input 
                type="number" 
                v-model.number="num2" 
                placeholder="Segundo número"
                class="number-input"
            >
        </div>

        <!-- Botões da calculadora -->
        <div class="calculator-buttons">
            <button @click="clear" class="btn operator">AC</button>
            <button @click="toggleSign" class="btn operator">+/-</button>
            <button @click="setOperation('percent')" class="btn operator">%</button>
            <button @click="setOperation('divide')" class="btn operator">÷</button>

            <button @click="appendNumber('7')" class="btn">7</button>
            <button @click="appendNumber('8')" class="btn">8</button>
            <button @click="appendNumber('9')" class="btn">9</button>
            <button @click="setOperation('multiply')" class="btn operator">×</button>

            <button @click="appendNumber('4')" class="btn">4</button>
            <button @click="appendNumber('5')" class="btn">5</button>
            <button @click="appendNumber('6')" class="btn">6</button>
            <button @click="setOperation('subtract')" class="btn operator">-</button>

            <button @click="appendNumber('1')" class="btn">1</button>
            <button @click="appendNumber('2')" class="btn">2</button>
            <button @click="appendNumber('3')" class="btn">3</button>
            <button @click="setOperation('add')" class="btn operator">+</button>

            <button @click="appendNumber('0')" class="btn zero">0</button>
            <button @click="appendDecimal" class="btn">.</button>
            <button @click="calculate" class="btn operator">=</button>
        </div>
    </div>
</template>

<script>
import CalculatorDisplay from "./CalculatorDisplay.vue";

export default {
    components: {
        CalculatorDisplay,
    },

    data() {
        return {
            currentInput: "",
            num1: 0,
            num2: 0,
            operation: "add",
            displayResult: "0"
        };
    },

    computed: {
        displayValue() {
            return this.displayResult;
        },
        calculatedResult() {
            const n1 = parseFloat(this.num1) || 0;
            const n2 = parseFloat(this.num2) || 0;

            let result;
            switch (this.operation) {
                case "add":
                    result = n1 + n2;
                    break;
                case "subtract":
                    result = n1 - n2;
                    break;
                case "multiply":
                    result = n1 * n2;
                    break;
                case "divide":
                    result = n2 !== 0 ? n1 / n2 : "Erro: Divisão por zero";
                    break;
                case "percent":
                    result = (n1 * n2) / 100;
                    break;
                default:
                    result = 0;
            }

            // Atualiza o display com o resultado
            this.displayResult = result.toString();
            return result;
        }
    },

    methods: {
        appendNumber(number) {
            if (!this.currentInput && number === '0') return;
            this.currentInput += number;
            this.updateFromCurrentInput();
        },

        setOperation(op) {
            this.operation = op;
            if (this.currentInput) {
                this.num1 = parseFloat(this.currentInput);
                this.currentInput = "";
            }
        },

        calculate() {
            if (this.currentInput) {
                this.num2 = parseFloat(this.currentInput);
            }
            const result = this.calculatedResult;
            this.currentInput = result.toString();
            this.num1 = parseFloat(this.currentInput);
            this.num2 = 0;
            this.displayResult = result.toString();
        },

        clear() {
            this.currentInput = "";
            this.num1 = 0;
            this.num2 = 0;
            this.operation = "add";
            this.displayResult = "0";
        },

        toggleSign() {
            if (this.currentInput) {
                this.currentInput = (parseFloat(this.currentInput) * -1).toString();
                this.updateFromCurrentInput();
            }
        },

        appendDecimal() {
            if (!this.currentInput.includes('.')) {
                this.currentInput = this.currentInput === '' ? '0.' : this.currentInput + '.';
            }
        },

        updateFromCurrentInput() {
            const value = parseFloat(this.currentInput);
            if (!isNaN(value)) {
                if (this.operation === "add" && this.num1 === 0) {
                    this.num1 = value;
                } else {
                    this.num2 = value;
                }
            }
        }
    },

    watch: {
        num1: {
            handler() {
                this.displayResult = this.calculatedResult.toString();
            }
        },
        num2: {
            handler() {
                this.displayResult = this.calculatedResult.toString();
            }
        },
        operation: {
            handler() {
                this.displayResult = this.calculatedResult.toString();
            }
        }
    }
};
</script>

<style scoped>
.calculator {
    width: 320px;
    background: #1c1c1c;
    border-radius: 20px;
    padding: 20px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.input-fields {
    display: grid;
    grid-template-columns: 2fr 1fr 2fr;
    gap: 5px;
    margin: 10px 0;
    padding: 8px;
    background: #333;
    border-radius: 10px;
    width: calc(100% - 16px);
}

.number-input {
    width: 100%;
    background: #444;
    border: none;
    padding: 8px 4px;
    color: white;
    border-radius: 5px;
    text-align: center;
    font-size: 14px;
    box-sizing: border-box;
}

.operation-select {
    width: 100%;
    background: #ff9500;
    border: none;
    color: white;
    padding: 4px;
    border-radius: 5px;
    font-size: 16px;
    text-align: center;
    cursor: pointer;
    box-sizing: border-box;
}

/* Removendo as setas do input number */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    appearance: none;
    margin: 0;
}

input[type=number] {
    -moz-appearance: textfield;
    appearance: textfield;
}

/* Resto dos estilos permanece igual */
.calculator-buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    padding-top: 10px;
}

.btn {
    background: #333;
    color: white;
    border: none;
    padding: 20px;
    font-size: 24px;
    border-radius: 50%;
    cursor: pointer;
    transition: background-color 0.2s;
}

.btn:hover {
    background: #404040;
}

.btn:active {
    background: #505050;
}

.operator {
    background: #ff9500;
}

.operator:hover {
    background: #ffaa33;
}

.zero {
    grid-column: span 2;
    border-radius: 35px;
    text-align: left;
    padding-left: 30px;
}
</style>