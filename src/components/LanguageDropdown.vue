<template>
    <v-select 
        class="language-dropdown"
        v-model="$i18n.locale"
        :on-change="updateLanguage()" 
        variant="outlined"
        :items="langs"
        item-text="title"
        item-value="tag"
        hide-details
    >
        <template v-slot:selection="{ item }">
            <img :src="generateUrlImg(item.value)" :alt="item.value">
        </template>
    </v-select>
</template>

<script lang="ts">
export default {
    data () {
      return {
        langs: [
            { title: 'English', tag: 'en' },
            { title: 'Français', tag: 'fr' }
        ],
      }
    },
    methods: {
        generateUrlImg: function(value: string) {
            return new URL(`/src/assets/${value}.png`, import.meta.url).href
        },
        updateLanguage() {
            localStorage.setItem("locale", this.$i18n.locale);
        },
    },
    mounted() {
        if (localStorage.getItem("locale")) {
            this.$i18n.locale = localStorage.getItem("locale")!;
        } else {
            localStorage.setItem("locale", this.$i18n.locale);
        }
    },
}
</script>

<style lang="scss" scoped>
@import '@/styles/variables.scss';
.language-dropdown {
    color: map-get($theme-color, "grey");
    font-family: "Montserrat", serif;
    max-width: 125px;
    position: fixed;
    right: 17px;
    top: 18px;
    z-index: 1;
}

.language-option {
    align-items: center;
    display: block;
}
</style>