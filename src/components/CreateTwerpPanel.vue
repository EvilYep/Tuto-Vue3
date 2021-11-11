<template>
    <form class="create-twerp-panel" 
        @submit.prevent="createNewTwerp" 
        :class="{ '--exceeded': newTwerpCharacterCount > 180 }">

        <label for="newTwerp"><strong>New Twerp</strong> ({{ newTwerpCharacterCount }}/180)</label>
        <textarea name="newTwerp" id="newTwerp" rows="4" v-model="newTwerpContent"></textarea>
            
        <div class="create-twerp-panel_submit">
            <div class="create-twerp-type">
                <label for="newTwerpType"><strong>Type: </strong></label>
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
                Twerp it !!
            </button>
        </div>
    </form>
</template>

<script>
export default {
    name: 'CreateTwerpPanel',

    data() {
        return {
            newTwerpContent: '',
            selectedTwerpType: 'instant',
            twerpTypes: [
                { value: 'draft', name: 'Draft'},
                { value: 'instant', name: 'Instant Twerp'},
            ],
        }
    },

    computed: {
        newTwerpCharacterCount() {
            return this.newTwerpContent.length;
        }
    },

    methods: {
        createNewTwerp() {
            if(this.newTwerpContent && this.selectedTwerpType !== 'draft') {
                this.$emit('add-twerp', this.newTwerpContent);
                this.newTwerpContent = '';
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.create-twerp-panel {
    margin-top: 20px;
    padding: 20px 0;
    display: flex;
    flex-direction: column;

    textarea {
        border: 1px solid #DFE3E8;
        border-radius: 5px;
    }

    .create-twerp-panel_submit {
        display: flex;
        justify-content: space-between;

        .create-twerp-type {
            padding: 10px 0;
        }

        button {
            padding: 5px 20px;
            margin: auto 0;
            border-radius: 5px;
            border: none;
            background-color: deeppink;
            color: white;
            font-weight: bold;
        }
    }

    &.--exceeded {
        color: red;
        border-color: red;

        .create-twerp-panel_submit {

            button {
                background-color: red;
                color: white;
            }
        }
    }
}
</style>