<template>
    <div>
        <div v-for="post in posts" :key="post">
            <pre>{{post.name}}</pre>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            posts: []
        }
    },

    async created () {
        const res = await fetch('https://swapi.dev/api/species/');
        const { results } = await res.json();
        this.posts = results;
    }
}
</script>