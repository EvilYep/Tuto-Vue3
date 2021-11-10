<template>
    <div id="main">
        <user-profile/>
    </div>
</template>

<script>
import UserProfile from './components/UserProfile'

export default {
    name: "App",

    components: {
        UserProfile
    }
};
</script>

<style>
body {
    margin: 0;
}

#main {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    min-height: 100vh;
    background-color: #f3f5fa;
}
</style>
