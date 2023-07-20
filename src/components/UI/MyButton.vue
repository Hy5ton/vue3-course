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
    font-family: Oswald;
    border: 0px solid #272A34;
    margin: 0;
    padding: 0;
    height: 20px;
    width: auto;
    font-size: 20px;
}
</style>
