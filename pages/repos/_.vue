<template>
    <div>
        Repo: {{ repo }} {{owner}}
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

        pathname = '/repos/octocat/Hello-World'
        
        // console.log(reponame);  
        const url = `https://api.github.com/repos/${pathname}`;

        this.$axios.get(url) 
        .then((resp) => {
            this.owner = resp.data.owner;
            console.log(resp.data)
        })
    }
}
</script>