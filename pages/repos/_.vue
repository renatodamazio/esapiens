<template>
    <div>
        <img :src="owner.avatar_url" :alt="owner.login" width="100px" height="100px" class="avatar">
        Repo: {{ repo.name }} 

        {{ repo.watchers }}

        {{ repo.clone_url }}

        {{ repo.watchers_count }}

        {{ repo.description }}

        {{ repo.language }}

        {{ repo.license }}

        {{ repo.stargazers_count }}
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            repo: [],
            owner: []
        }
    },

    mounted() {
        let pathname = window.location.pathname;
        const url = `https://api.github.com${pathname}`;

        this.$axios.get(url) 
        .then((resp) => {
            this.owner = resp.data.owner;
            this.repo = resp.data;
            // console.log(resp.data)
        })
    }
}
</script>