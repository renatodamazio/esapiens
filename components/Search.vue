<template>
    <div class="search-wrapper">
        <div class="input-search-container">
            
            <nuxt-link :to="`/`" class="github-logo">
                <img src="/gitlogo.png" width="40px" height="40px">
            </nuxt-link>

            <div class="input-search-wrapper">
                <img v-if="loading" src="/loading.gif" width="15px" height="15px" class="loading" alt="">
                <input type="text" class="search" autofocus v-model="username"  v-debounce:400ms="searchByUser" placeholder="Pesquisar por:" />
            </div>
        </div>
        <ul class="search-list" v-if="total > 0">
            <li class="total" v-if="total">Total &nbsp; <b>{{total}}</b></li>

            <li v-for="(user, i) in userlist" :key="i" @click="total = 0">
                <nuxt-link :to="`/user/${user.login}`">    
                        <img :src="user.avatar_url" class="avatar" width="30px" height="30px"/>
                        {{ user.login }}
                </nuxt-link>
            </li>

            <li v-if="!userlist" class="no-results">
                Não encontramos nenhum resultado para &nbsp;<b> "{{ username }}"</b>
            </li>
        </ul>
    </div>
</template>
<style scoped>
    .search-wrapper {
        padding: var(--space-md);
        z-index: 9999;
        border-bottom: 1px solid #eee;
    }

    .input-search-container {
        display: flex;
        align-items: center;
        width: 100%;
    }

    .loading {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        left: var(--space-sm);
    }

    .input-search-wrapper {
        position: relative;
        width: 100%;
    }

    .input-search-container img {
        margin-right: var(--space-md);
    }

    .no-results {
        padding: var(--space-lg);
        justify-content: center;
    }
    
    .search {
        border: 1px solid rgb(var(--color-dark));
        padding: var(--space-md) var(--space-lg);
        border-radius: 4px;
        width: 100%;
        transition: var(--transition-default);
    }

    .search:focus {
        border: 1px solid rgb(var(--color-primary));
        box-shadow: 0px 0px 6px rgb(var(--color-primary));
    }

    ul, li, a {
        width: 100%;
    }

    ul.search-list {
        padding: var(--space-md);
        border: 1px solid rgb(var(--color-primary-light));
        border-radius: 3px;
        position: absolute;
        width: 100%;
        background: #fff;
        left: 0;
        z-index: 999;
        top: 77px;
        height: calc(100% - 80px);
        overflow: auto;
        box-shadow: 0px 0px 5px rgb(var(--color-primary-light));
    }

    li, a {
        display: flex;
        align-items: center;
        border-bottom: 1px solid rgb(var(--color-primary-light));
    }

    .total {
        font-size: var(--text-sm);
    }

    a, .total {
        padding: var(--space-sm);
    }

    a:hover {
        background: rgb(var(--color-primary-light));
    }

    .avatar {
        margin-right: 8px;
    }

    .github-logo {
        width: 80px;
    }
</style>
<script>
import Vue from 'vue'
import vueDebounce from 'vue-debounce'
 
Vue.use(vueDebounce);

export default {
    data() {
        return {
            username: '',
            userlist: [],
            total: 0,
            loading: false
        }
    },
    
    mounted() {
        this.searchByUser();
    },

    methods: {
        searchByUser() {
            if (this.username.length == 0) {
                this.userlist = [];
                this.total = 0;
                return;
            };

            this.userlist = [];
            this.loading = true;

            const url = `https://api.github.com/search/users?q=${this.username}`
            this.$axios.get(url)
                .then((resp) => {
                    this.total = (resp.data.items).length;
                    
                    if (this.total == 0) {
                    
                        this.userlist = false;
                    
                    } else {

                        this.userlist = (resp.data.items);

                    }

                    this.loading = false;
                })
                .catch((err) => {
                    console.log(err)
                })
            }
    }
}
</script>