<template>
    <div id="main">
        <nav>
            <router-link :to="{ name: 'Home' }">
                <div class="navigation_logo">
                    Twerp
                </div>
            </router-link>
            <div class="navigation_user" v-if="user">
                {{ user.username }}
            </div>
        </nav>
        <router-view/>
    </div>
</template>

<script setup>
import { computed } from 'vue';
import { useStore } from 'vuex';

const store = useStore();
const user = computed(() => store.state.User.user);
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
