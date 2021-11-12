<template>
    <div class="twerp-item" @click="favouriteTwerp(twerp.id)">
        <div class="user-profile_twerp">
            <div class="twerp-item_user">
                @{{ username }}
            </div>
            <div class="twerp-item_content">
                {{ twerp.content }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TwerpItem',

    props: {
        username: {
            type: String,
            required: true
        },
        twerp: {
            type: Object,
            required: true
        }
    },

    setup(props, ctx) {
        function favouriteTwerp(id) {
            ctx.emit('favourite', id);
        }

        return {
            favouriteTwerp
        }
    }
}
</script>

<style lang="scss" scoped>
.twerp-item {
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    box-sizing: border-box;
    cursor: pointer;
    transition: all 0.25s ease-in-out;

    &:hover {
        transform: scale(1.1, 1.1);
    }

    .twerp-item_user {
        font-weight: bold;
    }
}
</style>