<script setup>

    import { Form, Field, ErrorMessage } from 'vee-validate';
    import * as yup from 'yup';

    const schema = yup.object({
        title: yup.string(),
        price: yup.number().typeError('Должно быть числом'),
    });

    const catalogItemSearchTitle = defineModel('title');
    const catalogItemSearchPrice = defineModel('price');

    const emit = defineEmits(['searchItem']);
    function onSearch(values){
        emit('searchItem', values);
    }
</script>

<template>
    <div class="search__block">
        <Form @submit="onSearch" :validation-schema="schema">
            <label>Введите назваение<Field name="title" type="text" v-model="catalogItemSearchTitle" /><ErrorMessage name="price" /></label>
            <label>Введите цену<Field name="price" type="text" v-model="catalogItemSearchPrice" /></label>
            <button type="submit">Поиск</button>
        </Form>
    </div>
</template>

<style scoped>
    .search__block{
        height: 100%;
        width: 100%;
    }
    .search__block input{
        font-size: 16px;
        margin-left: 10px;
    }
    .search__block button{
        margin-left: 20px;
    }
    .search__block label{
        margin-left: 20px;
    }
</style>