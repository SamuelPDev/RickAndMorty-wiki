<template>
    <section>
        <div class="characters">
            <div class="characters_items" v-for="character in  characters" :key="character.name">
                <CardCharacter :character="character" />
            </div>
        </div>
    </section>
</template>
<script>
import { computed, onMounted } from "vue";
import { useStore } from 'vuex';
import CardCharacter from "./CardCharacter.vue";

export default {
    setup() {
        const store = useStore();
        const characters = computed(() => {
            return store.state.charactersFilter;
        });
        onMounted(() => {
            store.dispatch("getCharacters");
        });
        return {
            characters
        };
    },
    components: {
        CardCharacter
    }
}
</script>
<style lang="scss">
.characters {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 3rem;
    margin: 3rem 0;
}
</style>

