<template>
    <div class="container">
        <user-aside :user="owner"/>
        <aside class="aside-bar">
            <h1 class="title mb-sm flex justify-between"> 
                <a :href="repo.html_url" target="_blank">{{owner.login}}/{{ repo.name }} </a>

                <div class="flex justify-between">
                    <span class="tag"><i class="fa fa-eye pr-sm"></i> Watchers | {{ repo.watchers }}</span>

                    <span class="tag"><i class="fa fa-star pr-sm"></i>Stars | {{ repo.stargazers_count }}</span>
                </div>    
            </h1>

            <hr class="mb-lg mt-lg"> 

            <div class="section flex" :class="source ? ' justify-between' : 'justify-end'">
                <div v-if="source">
                    <i class="fas fa-code-branch"></i>
                    {{ source.default_branch }}
                </div>              
            </div>
            
            <div class="section about-project">
                <h2 class="title-about">Sobre o projeto</h2>
                
                {{ repo.description }}

                <ul class="list-default">
                    <li>
                        <a :href="repo.html_url" target="_blank"><i class="fa fa-external-link-alt pr-sm"></i>Acessar projeto</a>
                    </li>
                    <li>
                        <b><i class="fa fa-code icon pr-sm"></i> Linguagem:</b> {{ repo.language }}
                    </li>
                    <li v-if="repo.license">
                        <b><i class="fas fa-gavel icon pr-sm"></i>Licença:</b> {{ repo.license.name }}
                    </li>
                </ul>
            </div>
        </aside>
    </div>
</template>

<style scoped>
    .container {
        display: flex;
    }

    .aside-bar {
        flex-grow: 1;
    }

    .title {
        width: 100%;
        align-items: center;
    }

    .title a {
        color: rgb(var(--color-primary));
        position: relative;
    }

    .fa-star {
        color: rgb(var(--color-warning));
    }

    .fa-eye {
        color: rgb(var(--color-primary));
    }

    .tag {
        font-size: 12px;
        padding: var(--space-sm) var(--space-lg);
        border: 1px solid #eee;
        display: inline-block;
        margin: 0 var(--space-sm);
        background: rgb(238 238 238 / 31%);
    }

    .about-project {
        width: 100%;
        float: left;
        border-top: 1px solid rgb(var(--color-primary-ligth));
        margin-top: var(--space-md);
        padding: var(--space-lg) 0;
    }

    .title-about {
        padding-bottom: var(--space-md);
    }

    .list-default li {
        font-size: 14px;
    }

    .list-default li b {
        opacity: 0.5;
    }


     @media only screen and (max-width: 800px) {
        .container {
            flex-direction: column;
        }

        h1 a {
            margin-bottom: var(--space-md);
        }
    
        .title {
            word-break: break-all;
            flex-direction: column;
        }

        .tag {
            display: flex;
            margin: 4px;
        }
    }

</style>

<script>
import axios from 'axios';

export default {
    head() {
        return {
            title: 'Detalhes do repositório'
        }
    },
    data() {
        return {
            repo: [],
            source: [],
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
            this.source = this.repo.source;
            // console.log(resp.data)
        })
    }
}
</script>