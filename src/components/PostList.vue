<template>
    <div v-if="posts.length > 0">
        <!-- мб вернуть анимации добавления-удаления -->
            <post-item 
            v-for:="post in posts"
            :post="post"
            :key="post.id"
            @remove="$emit('remove', post)"
            />
        
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

</style>