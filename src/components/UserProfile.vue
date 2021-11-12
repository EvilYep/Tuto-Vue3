<template>
    <div class="user-profile">

        <div class="user-profile_sidebar">
            <div class="user-profile_user-panel">
                <h1 class="user-profile_username">@{{ state.user.username }}</h1>
                <div class="user-profile_admin-badge" v-if="state.user.isAdmin">
                    Admin
                </div>
                <div class="user-profile_followers-count">
                    <strong>Followers :</strong> {{ state.followersCount }}
                </div>
            </div>

            <create-twerp-panel @add-twerp="addTwerp"/>

        </div>

        <div class="user-profile_twerps-wrapper">
            <twerp-item 
                v-for="twerp in state.user.twerps" 
                :key="twerp.id" 
                :username="state.user.username" 
                :twerp="twerp"
                @favourite="toggleFavourite"
            />
        </div>
    </div>
</template>

<script>
import { onMounted, reactive, watch } from "vue";
import CreateTwerpPanel from './CreateTwerpPanel';
import TwerpItem from './TwerpItem';

export default {
    name: 'UserProfile',

    components: {
        TwerpItem,
        CreateTwerpPanel
    },

    setup() {
        const state = reactive({
            followersCount: 0,
            user: {
                id: 1,
                username: '_Yep',
                firstName: 'Yep',
                lastName: 'Derp',
                email: 'yep@derp.com',
                isAdmin: true,
                twerps: [
                    { id: 1, content: 'You know what ?' },
                    { id: 2, content: 'I am Happy !' },
                ]
            }
        });

        // So useful : https://www.netlify.com/blog/2021/01/29/deep-dive-into-the-vue-composition-apis-watch-method/
        watch(() => state.followersCount, (newCount, oldCount) => {
            if(oldCount < newCount) {
                console.log(`${state.user.username } has gained a follower !`);
            }
        })

        function followUser() {
            state.followersCount++;
        }

        function toggleFavourite(id) {
            console.log(`Favourited Twerp #${id}`);
        }

        function addTwerp(twerp) {
            state.user.twerps.push({ id: state.user.twerps.length + 1, content: twerp });
        }

        onMounted(() => {
            followUser();
        })

        return {
            state,
            followUser,
            toggleFavourite,
            addTwerp,
        }
    }
}
</script>

<style lang="scss" scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    gap: 50px;
    padding: 50px 5%;

    .user-profile_user-panel {
        display: flex;
        flex-direction: column;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid #dfe3e8;

        h1 {
            margin: 0;
        }

        .user-profile_admin-badge {
            background-color: rebeccapurple;
            color: white;
            border-radius: 5px;
            margin-right: auto;
            padding: 0 10px;
            font-weight: bold;
        }

        .user-profile_followers-count {
            padding-bottom: 20px;
        }
    }

    .user-profile_twerps-wrapper {
        display: grid;
        gap: 10px;
    }
}
</style>