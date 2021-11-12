<template>
    <div id="main">
        <nav>
            <div class="navigation_logo">
                Twerp
            </div>
            <div class="navigation_user">
                {{ state.user.username }}
            </div>
        </nav>
        <user-profile/>
    </div>
</template>

<script>
import { reactive } from 'vue';
import UserProfile from './components/UserProfile'

export default {
    name: "App",

    components: {
        UserProfile
    },

    setup() {
        const state = reactive({
            user: {
                username: '_Yep'
            }
        });

        return {
            state
        }
    },
};
</script>

<style lang="scss">
body {
    margin: 0;
}

a {
    color: inherit;
    text-decoration: none;
}

#main {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    min-height: 100vh;
    background-color: #F3F5FA;

    nav {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px 5%;
        background-color: deeppink;
        color: white;

        .navigation_logo {
            font-weight: bold;
            font-size: 24px;
        }

        .navigation_user {
            font-weight: bold;
        }
    }
}
</style>
