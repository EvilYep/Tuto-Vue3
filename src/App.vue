<template>
    <div id="app">
        @{{ user.username }} - {{ fullName }}
        <strong>followers: </strong> {{ followersCount }}
        <button @click="followUser">
            Follow
        </button>
    </div>
</template>

<script>
export default {
    name: "App",

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
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    display: flex;
    flex-direction: column;
    text-align: center;
}
</style>
