<template>
    <div class="calculator-buttons">
        <button @click="$emit('append-number', 7)">7</button>
        <button @click="$emit('append-number', 8)">8</button>
        <button @click="$emit('append-number', 9)">9</button>
        <button @click="$emit('set-operation', 'subtract')" class="action">−</button>

        <button @click="$emit('append-number', 4)">4</button>
        <button @click="$emit('append-number', 5)">5</button>
        <button @click="$emit('append-number', 6)">6</button>
        <button @click="$emit('set-operation', 'add')" class="action">+</button>

        <button @click="$emit('append-number', 1)">1</button>
        <button @click="$emit('append-number', 2)">2</button>
        <button @click="$emit('append-number', 3)">3</button>
        <button @click="$emit('calculate')" class="equals">=</button>

        <button @click="$emit('append-number', 0)" class="zero">0</button>
        <button @click="$emit('append-number', '.')" :disabled="hasDecimal">.</button>
    </div>
</template>

<script>
export default {
    props: {
        hasDecimal: {
            type: Boolean,
            default: false
        }
    },
    emits: ['append-number', 'set-operation', 'calculate', 'clear']
}
</script>

<style>
.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

button {
    background: #4a4a4a;
    color: #ffffff;
    font-size: 1.5rem;
    padding: 10px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}

button:hover {
    background: #606060;
}

.action {
    background: #ff9500;
}

.action:hover {
    background: #e08900;
}

.equals {
    grid-column: span 2;
    background: #00ff7f;
}

.equals:hover {
    background: #00e067;
}

.zero {
    grid-column: span 2;
}
</style>