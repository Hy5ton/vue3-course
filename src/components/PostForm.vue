<template>
    <form @submit.prevent >
            <h2>Create item</h2>
            <my-input class="new--item"
            v-model="post.title"
            type="text" 
            placeholder="Title item"
            />
            <my-input class="new--item"
            v-model="post.body"
            type="text" 
            placeholder="Description item"
            />
            <my-input class="new--item"
            v-model="post.type"
            type="text"
            placeholder="Type item"
            />
            <my-input class="new--item"
            v-model="post.price"
            type="text"
            placeholder="Price item"
            />
            <my-input class="new--item"
            v-model="post.src"
            type="text"
            placeholder="Link to image"
            />
            <my-button class="crt--btn"
            style="align-self: flex-end; margin-top: 15px; color: white;" 
            @click="createPost"> 
            Create new item 
            </my-button>
        </form>
</template>

<script>
import MyInput from './UI/MyInput.vue';

export default {
  components: { MyInput },
    data() {
        return {
            post: {
                title: '',
                body: ''
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now;
            this.$emit('create', this.post)
            this.post = {
            title: '',
            body: ''
            }
        }
    },
}
</script>

<style scoped>
form{
    font-family: Oswald;
    position: relative;
    z-index: 9999;
    font-size:20px;
    font-weight: 700;
    color: white;
    width: 800px;
    display: flex;
    flex-direction: column;
}
.crt--btn{
    color:white;
    cursor: pointer;
}
.new--item{
    font-family: Oswald;
}
</style>