<template>
    <div class="display">{{ value || '0' }}</div>
</template>

<script>
export default {
    props: {
        value: {
            type: [String, Number],
            default: '0'
        }
    }
}
</script>

<style scoped>
.display {
    background: #1c1c1c;
    color: white;
    text-align: right;
    padding: 30px 20px;
    font-size: 48px;
    font-weight: 300;
    margin-bottom: 10px;
    overflow: hidden;
    text-overflow: ellipsis;
}
</style>