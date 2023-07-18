<template>
    <div v-if="posts.length > 0">
        <transition-group name="post-list">
            <post-item 
            v-for:="post in posts"
            :post="post"
            :key="post.id"
            @remove="$emit('remove', post)"
            />
        </transition-group>
        
    </div>
    <h1 v-else style="color: rgb(101, 189, 101)">
        Items empty
    </h1>
</template>

<script>
import PostItem from "./PostItem.vue"

export default {
    components: { PostItem },
    props: {
        posts: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style scoped>
.post-list-item {
    display: inline-block;
    margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
    transition: all 0.5s ease;
}
.post-list-enter-from,
.post-list-leave-to {
    opacity: 0;
    transform: translateY(130px);
}
.post-list-move {
    transition: transform 0.7s ease;
}
</style>