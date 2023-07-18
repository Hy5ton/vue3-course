<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>

export default {
    name: 'my-button'
}
</script>

<style scoped>
.btn{
    border: 1px solid #373943;
    width: 182px;
    height: 60px;
    font-size: 20px;
}
</style>
