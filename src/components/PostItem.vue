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
    cursor: pointer;
    border-style: solid;
    border-width: 2px;
    border-color: var(--green, #38F2AF);
    border-radius: 25px;
    justify-content: center; 
    text-align: center;
    align-items: center;
    width: 132px;
    height: auto;
    margin-bottom: 20px;
    position: relative;
    z-index: 1;
    left: 190px;
    top: 100px;
    margin: 0;
    padding-top: 2px;
    padding-bottom: 4px;
}
.post_btns{
    position: relative;
    text-align: left;
    height: 15px;
    margin-top: 65px;
}
.type--delete--btns--style{
    width: 150px;
    color:var(--green, #38F2AF);;
}
</style>
