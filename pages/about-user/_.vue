<template>
    <div>
        <div class="user-info">
            <img :src="user.avatar_url" width="120px" height="120px" class="avatar">
            <h2>{{ user.name }}</h2>
            <a :href="user.html_url" target="_blank">Perfil</a>
            <hr>
            {{ user.bio }}

            {{ user.location }}

            {{ user.company }}

            {{ user.public_repos }}

            {{ user.followers }}

            {{ user.following }}
        </div>

        <aside class="repos">
            Repositórios.
            <ul>
                <li v-for="(repo, key) in repos" :key="key">
                    <nuxt-link :to="`/repo/${repo.full_name}`">
                        {{ repo.name }} {{ repo.stargazers_count }}

                        {{ repo.description }}
                    </nuxt-link>
                </li>
            </ul>
        </aside>
    </div>
</template>

<style scoped>
    .repos ul {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        padding: 16px;
    }

    .repos ul li {
        width: 50%;
        flex: 1 0 auto;
        padding: 24px;
        padding: 4px; 
        list-style: none;
    }

    .repos ul li a {
        border: 1px solid #eee;
        padding: 24px;
        width: 100%;
        border-radius: 8px;
        float: left;
    }
</style>
<script>
import axios from 'axios';
export default {
    head() {
        return {
            title: 'Github - About user'
        }
    },

    data() {
        return {
            user: [],
            repos: []
        }
    },

    mounted() {
        let pathname = window.location.pathname,
            slices = (pathname.split('/')),
            username = slices[slices.length -1];

        const getRepos = axios.get(`https://api.github.com/users/${username}/repos`);
        const getUser = axios.get(`https://api.github.com/users/${username}`);

        axios.all([getUser, getRepos])
        .then(axios.spread((...responses) => {

            var user = responses[0];
            var repo = responses[1];

            repo.data.sort((a, b) => {
                return a.stargazers_count - b.stargazers_count;
            });

            this.repos = repo.data;
            this.user = user.data;
        }))
    }
}
</script>