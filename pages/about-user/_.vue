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
            <draggable v-model="repos" class="list-group" tag="ul">
                <transition-group type="transition" :name="!drag ? 'flip-list' : null">
                    <div v-for="(repo, key) in repos" :key="key" class="list-group-item">
                        <nuxt-link :to="`/repos/${repo.full_name}`">
                            {{ repo.name }} {{ repo.stargazers_count }}

                            {{ repo.description }}
                        </nuxt-link>
                    </div>
                </transition-group>
            </draggable>
        </aside>
    </div>
</template>

<style scoped>
    .repos {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        padding: 16px;
    }

    .repos .items {
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

    .flip-list-move {
        transition: transform 0.5s;
        }
        .no-move {
        transition: transform 0s;
        }
        .ghost {
        opacity: 0.5;
        background: #c8ebfb;
        }
        .list-group {
        min-height: 20px;
        }
        .list-group-item {
        cursor: move;
        }
        .list-group-item i {
        cursor: pointer;
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
            repos: [],
            drag: false
        }
    },

    components: {
        draggable: () => import('vuedraggable')
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