<template>
    <div>
        <input type="search" v-model="username"  v-debounce:400ms="searchByUser" placeholder="Pesquisar por:" />
        <ul>
            <li v-for="(user, i) in userlist" :key="i">
                <nuxt-link :to="`/about-user/${user.login}`">    
                        <img :src="user.avatar_url" class="avatar" width="30px" height="30px"/>
                        {{ user.login }}
                </nuxt-link>
            </li>
        </ul>
    </div>
</template>
<style scoped>
    ul, li, a {
        width: 100%;
    }

    li, a {
        display: flex;
        align-items: center;
        border: 1px solid #000;
    }

    a {
        padding: 8px;
    }

    .avatar {
        margin-right: 8px;
    }
</style>
<script>
export default {
    data() {
        return {
            username: 'renato damázio',
            userlist: []
        }
    },

    mounted() {
        console.log(this.searchByUser());
    },

    methods: {
        searchByUser() {
            if (this.username.length == 0) {
                this.userlist = [];
                return;
            }

            const url = `https://api.github.com/search/users?q=${this.username}`
            this.$axios.get(url)
                .then((resp) => {
                    console.log(resp.data.items);
                    this.userlist = (resp.data.items)
                })
                .catch((err) => {
                    console.log(err)
                })
            }
    }
}
</script>