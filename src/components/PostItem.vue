<template>
<div class="post"
    @click="showPost()">
    <div>
        <div class="imagePost"><img :src="post.src"></div>
        <div class="titlePost"><strong> </strong> {{ post.title }}</div>
        <div class="descriptionPost"><strong> </strong> {{ post.body }}</div>
        <div class="pricePost" 
        @click="showDialog">{{ post.price }}</div>
    </div>
    <div class="post_btns">
        <my-button class="type--delete--btns--style"
        @click="$emit('remove', post)"
        >{{post.type}}
        </my-button>
    </div>  
</div>
<item-dialog @hideDialog="showPostFlag=false" v-if="showPostFlag" :post="post"></item-dialog>
<!-- проблема тут -->
</template>

<script>

import ItemDialog from './UI/ItemDialog.vue';

export default {
    data(){
        return {
            showPostFlag: false
        }
    },
    components:{
        ItemDialog
    },
    props: {
       post: {
         type: Object,
         required: true,
       }
    },
    methods:{
        showPost(){
            this.showPostFlag = true
        }
    },
}
</script>

<style scoped>
.post{
    padding: 15px;
    margin-top: 15px;
    display: inline-block;
    align-items: center;
    justify-content: space-between;
    width: 358px;
    height: 500px;
    margin: 20px 14px;
    border-radius: 10px;
}
.imagePost{
    width: 100%;
}
.titlePost{
    font-size: 30px;
    margin-top: 20px;
}
.descriptionPost{
    font-size: 20px;
    margin-top: 10px;
    color: gray;
    margin-bottom: 10px;
}
.pricePost{
    border-style: solid;
    border-width: 2px;
    border-color: var(--green, #38F2AF);
    border-radius: 25px;
    text-align: center;
    line-height:  40px;
    width: 132px;
    height: 40px;
    margin-bottom: 20px;
    position: relative;
    z-index: 1;
    left: 190px;
    top: 120px;
}
.post_btns{
    width: 132px;
    height: 40px;
    margin-top: 70px;
}
.type--delete--btns--style{
    color:var(--green, #38F2AF);;
}
</style>
