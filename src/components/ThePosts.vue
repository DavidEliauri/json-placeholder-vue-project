<script setup>
    import axios from 'axios';
    import PostCard from '@/components/PostCard.vue';
    import { onMounted, ref } from 'vue';

    const users = ref([]);
    const posts = ref([]);

    onMounted(async () => {
        const getUsersResponse = await axios.get('https://jsonplaceholder.typicode.com/users');

        users.value = getUsersResponse.data;

        const getPostsResponse = await axios.get('https://jsonplaceholder.typicode.com/posts');

        posts.value = getPostsResponse.data;
    });
</script>

<template>
    <div class="columns-2 lg:columns-3">
        <div
            v-for="post in posts"
            :key="post.id"
            class="mb-6 break-inside-avoid-column"
        >
            <PostCard
                :title="post.title"
                :description="post.body"
                :author="
                    users.find((u) => {
                        return u.id === post.userId;
                    }).name
                "
            />
        </div>
    </div>
</template>
