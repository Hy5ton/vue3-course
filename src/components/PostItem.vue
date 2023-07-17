<template>
    <div class="post">
        <div>
            <div class="imagePost"><img :src="post.src"></div>
            <div class="titlePost"><strong> </strong> {{ post.title }}</div>
            <div class="descriptionPost"><strong> </strong> {{ post.body }}</div>
        </div>
        <div class="post_btns">
            <my-button
            @click="$emit('remove', post)"
            >Delete
        </my-button>
        </div>  
</div>
</template>

<script>

export default {
    props: {
       post: {
         type: Object,
         required: true,
       } 
    }
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
</style>
