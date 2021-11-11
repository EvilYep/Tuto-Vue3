<template>
    <div class="user-profile">

        <div class="user-profile_user-panel">
            <h1 class="user-profile_username">@{{ user.username }}</h1>
            <div class="user-profile_admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user-profile_followers-count">
                <strong>Followers :</strong> {{ followersCount }}
            </div>

            <form class="user-profile_create-twerp" 
                @submit.prevent="createNewTwerp" 
                :class="{ '--exceeded': newTwerpCharacterCount > 180 }">

                <label for="newTwerp"><strong>New Twerp</strong> ({{ newTwerpCharacterCount }}/180)</label>
                <textarea name="newTwerp" id="newTwerp" rows="4" v-model="newTwerpContent"></textarea>
                
                <div class="user-profile_create-twerp-type">
                    <label for="newTwerpType"><strong>Type </strong></label>
                    <select name="newTwerpType" id="newTwerpType" v-model="selectedTwerpType">
                        <option 
                            v-for="(option, index) in twerpTypes" 
                            :value="option.value"
                            :key="index"
                        >
                            {{ option.name }}
                        </option>
                    </select>
                
                </div>

                <button>
                    Twerp !!
                </button>
            </form>
        </div>

        <div class="user-profile_twerps-wrapper">
            <twerp-item 
                v-for="twerp in user.twerps" 
                :key="twerp.id" 
                :username="user.username" 
                :twerp="twerp"
                @favourite="toggleFavourite"
            />
        </div>
    </div>
</template>

<script>
import TwerpItem from './TwerpItem';

export default {
    name: 'UserProfile',

    components: {
        TwerpItem
    },

    data() {
        return {
            newTwerpContent: '',
            selectedTwerpType: 'instant',
            twerpTypes: [
                { value: 'draft', name: 'Draft'},
                { value: 'instant', name: 'Instant Twerp'},
            ],
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
        newTwerpCharacterCount() {
            return this.newTwerpContent.length;
        }
    },

    methods: {
        followUser() {
            this.followersCount++;
        },
        toggleFavourite(id) {
            console.log(`Favourited Twerp #${id}`);
        },
        createNewTwerp() {
            if(this.newTwerpContent && this.selectedTwerpType !== 'draft') {
                this.user.twerps.push({
                    id: this.user.twerps.length + 1,
                    content: this.newTwerpContent
                });
                this.newTwerpContent = '';
            }
        }
    },

    mounted() {
        this.followUser();
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

        .user-profile_create-twerp {
            border-top: 1px solid #dfe3e8;
            padding-top: 20px;
            display: flex;
            flex-direction: column;

            &.--exceeded {
                color: red;
                border-color: red;
                border: none;

                button {
                    background-color: red;
                    border: none;
                    color: white;
                }
            }

            .user-profile_create-twerp-type{
                padding-top: 5px;
                padding-bottom: 5px;
            }
        }
    }

    .user-profile_twerps-wrapper {
        display: grid;
        gap: 10px;
    }
}
</style>