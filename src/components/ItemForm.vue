<template>
    <form @submit.prevent>
        <div class="dialog__item" @click.stop="hideDialog">
            <div @click.stop class="dialog__content__item">
                <div class="imagePost"><img class="imagePost--style" :src="post.src"></div>
                <div class="titlePost"><strong> </strong> {{ post.title }}</div>
                <div class="descriptionPost"><strong> </strong> {{ post.body }}</div>
                <div class="typePost"><strong> </strong> {{ post.type }}</div>
                <div class="pricePost"><strong> </strong> {{ post.price }}</div>
            </div>
        </div>
    </form>
</template>

<script>
import MyInput from './UI/MyInput.vue';
import ItemDialog from './UI/ItemDialog.vue';
export default {
}
</script>

<style scoped>
form{
    position: relative;
    z-index: 9999;
    font-size:20px;
    font-weight: 700;
    color: white;
    width: 800px;
    display: flex;
    flex-direction: column;
}

</style>