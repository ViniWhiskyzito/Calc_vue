<template>
    <div class="reactive-fields">
        <input 
            :value="num1"
            @input="$emit('update:num1', $event.target.value)" 
        />
        <select 
            :value="operation"
            @change="$emit('update:operation', $event.target.value)"
        >
            <option value="add">+</option>
            <option value="subtract">-</option>
            <option value="multiply">×</option>
            <option value="divide">÷</option>
        </select>
        <input 
            :value="num2"
            @input="$emit('update:num2', $event.target.value)" 
        />
    </div>
</template>

<script>
export default {
    props: {
        num1: {
            type: Number,
            required: true
        },
        num2: {
            type: Number,
            required: true
        },
        operation: {
            type: String,
            required: true
        }
    },
    emits: ['update:num1', 'update:num2', 'update:operation']
}
</script>

<style>
.reactive-fields {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 20px;
}

.number-input,
.operation-select {
    width: 100%;
    padding: 10px;
    font-size: 1.2rem;
    border: none;
    border-radius: 6px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}

.operation-select {
    background-color: #4a4a4a;
    color: #ffffff;
}

.number-input:focus,
.operation-select:focus {
    outline: none;
    border: 2px solid #00ff7f;
}
</style>