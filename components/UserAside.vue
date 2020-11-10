<template>
    <div>
        <div class="user-info">
            <img :src="user.avatar_url" width="180px" height="180px" class="avatar">
            <div class="user-bio"> 
                <h2 class="text-center">{{ user.name }}</h2>
                <p class="user-login text-center">{{ user.login }}</p>
                <hr>
                <div class="user-info-counters">
                    <div v-if="user.bio" class="user-info-small">
                        {{ user.bio }}
                    </div>

                    <div  v-if="user.location" class="user-info-small">
                        <i class="fas fa-map-marker-alt icon"></i> {{ user.location }}
                    </div>
                    
                    <div v-if="user.email" class="user-info-small">
                        <i class="fa fa-envelope icon"></i>
                        {{ user.email }}
                    </div>
                    
                    <div v-if="user.company" class="user-info-small">
                        <i class="fa fa-building icon"></i>
                        {{ user.company }} 
                    </div>
                    
                    <div class="user-info-small" v-if="user.following || user.followers">
                        <i class="fa fa-user-friends icon"></i>&nbsp;{{ user.followers }} Seguidores
                        -
                        {{ user.following }} Seguindo
                        
                        {{ user.stargazers_count }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        user: {
            default: []
        }
    }
}
</script>

<style scoped>
     .user-info-small {
        width: 100%;
        float: left;
        display: flex;
        align-items: center;
        padding-bottom: var(--space-sm);
        flex-direction: row;
    }

    hr {
        margin: 10px 0;
    }

    .user-bio {
        text-align: left;
        font-size: var(--text-sm);
    }

    .avatar {
        border: 2px solid;
    }

    .user-login {
        font-weight: 400;
        opacity: 0.8;
    }

    .user-info {
        min-width: 280px;
        display: inline-block;
        text-align: center;
        padding: var(--space-md);
    }

    .user-info-counters {
        font-size: var(--text-sm);
        padding: var(--space-md) 0;
    }

    .repos {
        padding: var(--space-md) 0;
    }

    .repo-title {
        color: rgb(var(--color-primary));
        font-size: var(--text-base);
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .icon {
        width: 16px;
        text-align: center;
    }

    @media only screen and (max-width: 320px) {
        .user-info {
            width: 100%;
        }
    } 
</style>