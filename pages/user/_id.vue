<template>
    <div class="container">
        <user-aside :user="user"/>

        <aside class="repos">
            <h3 class="title">{{ user.public_repos }} Repositórios.</h3>
            <draggable v-model="repos" class="list-group" tag="ul">
                <transition-group type="transition" :name="!drag ? 'flip-list' : null">
                    <div v-for="(repo, key) in repos" :key="key" class="list-group-item">
                        <nuxt-link :to="`/repos/${repo.full_name}`">
                            <h3 class="repo-title">
                                {{ repo.name }}
                                <i class="repo-status" :class="repo.disabled ? 'disabled' : ''"></i>
                            </h3> 
                            
                            <div class="repo-description">{{ repo.description ? repo.description : 'Sem descrição'  }}</div>

                            <div class="repo-footer">
                                <div class="repo-star"><i class="fa fa-star"></i>{{repo.stargazers_count}}</div>
                                <div class="repo-star" v-if="repo.language"><i class="fa fa-code"></i>{{repo.language}}</div>
                            </div>
                        </nuxt-link>
                    </div>
                </transition-group>
            </draggable>
        </aside>


        <nuxt-child/>
    </div>
</template>

<style scoped>
    .container {
        display: flex;
    }
    
    .repo-stars {
        color: rgb(var(--text-base))
    }

    .repo-star {
        font-size: var(--space-md);
    }

    .fa-star {
        color: rgb(var(--color-warning));
    }

    .repo-footer {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .repo-status {
        width: 8px;
        height: 8px;
        display: inline-block;
        background: rgb(var(--color-success));
        border-radius: 100%;
    }

    .repo-status.disabled {
        background: rgb(var(--color-danger));
    }

    .repo-star i {
        margin-right: var(--space-sm);
    }

    .title {
        padding: var(--space-sm);
    }

    .repo-description {
        color: rgb(var(--text-base));
        opacity: 0.8;
        flex-grow: 1;
        font-size: var(--text-sm);
        padding: var(--space-sm) 0;
    }

    .list-group > span {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }

    .list-group .list-group-item {
        width: 50%;
        flex: 1 0 auto;
        padding: 24px;
        padding: 4px; 
        background: #fff;
        list-style: none;
    }

    .list-group .list-group-item a {
        border: 1px solid #eee;
        padding: var(--space-md);
        height: 140px;
        width: 100%;
        display: flex;
        flex-direction: column;
        border-radius: 8px;
        float: left;
    }

    .list-group .list-group-item a:hover {
        background: var(--color-primary-light);
        box-shadow: 0px 0px 4px rgb(var(--color-primary-light));
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

    @media only screen and (max-width: 800px) {
        .container {
            flex-direction: column;
        }
    
        .list-group > span {
            flex-direction: column;
        }

        .list-group .list-group-item {
            width: 100%;
        }

        .repo-description {
            white-space: normal;
            word-break: break-word;
        }
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
        draggable: () => import('vuedraggable'),
        UserAside: () => import('@/components/UserAside.vue')
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