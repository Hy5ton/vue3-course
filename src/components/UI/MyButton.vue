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
    padding: 10px 15px;
    background: rgb(101, 189, 101);
    color: black;
    border: 1px solid gray;
    border-radius: 15px;
}
</style>
