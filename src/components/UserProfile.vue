<template>
    <div class="user-profile">
        <div class="user-profile_user-panel">
            <h1 class="user-profile_username">@{{ user.username }}</h1>
            <div class="user-profile_followers-count">
                <strong>Followers :</strong> {{ followersCount }}
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'UserProfile',

    data() {
        return {
            followersCount: 0,
            user: {
                id: 1,
                username: '_Yep',
                firstName: 'Yep',
                lastName: 'Derp',
                email: 'yep@derp.com',
                admin: true
            }
        }
    },

    watch: {
        followersCount(newCount, oldCount) {
            if(oldCount < newCount) {
                console.log(`${this.user.username} has gained a follower !`);
            }
        }
    },

    computed: {
        fullName() {
            return `${this.user.firstName} ${this.user.lastName}`
        }
    },

    methods: {
        followUser() {
            this.followersCount++;
        }
    },

    mounted() {
        this.followUser();
    }
}
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
}

h1.user-profile_username {
    margin: 0;
}
</style>