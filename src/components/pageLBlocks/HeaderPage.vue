<script setup>
    import { ref } from 'vue';
    import CatalogSearch from '../search/CatalogSearch.vue';

    const catalogItemSearchTitle = ref('');
    const catalogItemSearchPrice = ref(0);

    const emit = defineEmits(['showSearchItem']);
    function searchItem(value){
        emit('showSearchItem', value);
    }
</script>

<template>
    <CatalogSearch v-model:title="catalogItemSearchTitle" v-model:price="catalogItemSearchPrice" @searchItem="searchItem($event)"></CatalogSearch>
</template>

<style scoped>

</style>