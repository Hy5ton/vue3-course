<template>
<div class="dialog__item" @click.stop="hideDialog">
    <div @click.stop class="dialog__content__item">
        <div class="imagePost"><img class="imagePost--style" :src="post.src"></div>
        <div class="titlePost"><strong> </strong> {{ post.title }}</div>
        <div class="descriptionPost"><strong> </strong> {{ post.body }}</div>
        <div class="typePost"><strong> </strong> {{ post.type }}</div>
        <div class="pricePost"><strong> </strong> {{ post.price }}</div>
    </div>
</div>
</template>

<script>
export default {
    name: 'item-dialog',
    props: {
        post:{
            type: Object,
            default: null,
        }
    },
    methods: {
        hideDialog() {
            this.$emit('hideDialog', false)
        }
    },
}
</script>

<style scoped>
.dialog__item {
    position: relative;
    z-index: 9995;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    display: flex;
}
.dialog__content__item {
    margin: auto;
    border-radius: 12px;
    min-height: 800px;
    min-width: 600px;
    padding: 20px;
}
.imagePost--style{
    width: 100%;
    height: 100%;
    object-fit: contain;
}
.titlePost{
    font-size: 60px;
}
.descriptionPost{
    margin-top: 20px;
    font-size: 40px;
    color: gray;
}
.typePost{
    width: 232px;
    height: 40px;
    margin-top: 180px;
    font-size: 40px;
    color: #38F2AF;
}
.pricePost{
    border-style: solid;
    border-width: 2px;
    border-color: var(--green, #38F2AF);
    border-radius: 25px;
    text-align: center;
    line-height:  70px;
    width: 232px;
    height: 80px;
    margin-bottom: 20px;
    position: relative;
    z-index: 1;
    left: 330px;
    top: -40px;
    font-size: 40px;
}
</style>