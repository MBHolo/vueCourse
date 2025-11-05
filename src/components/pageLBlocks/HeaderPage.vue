<script setup>
    import { ref } from 'vue';
    import CatalogSearch from '../search/CatalogSearch.vue';

    const catalogItemSearch = ref('');

    const emit = defineEmits(['showSearchItem']);
    function searchItem(value){
        emit('showSearchItem', value);
    }
</script>

<template>
    <CatalogSearch v-model:searchData="catalogItemSearch" @searchItem="searchItem($event)"></CatalogSearch>
</template>

<style scoped>

</style>