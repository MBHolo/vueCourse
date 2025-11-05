<script setup>

    import { Form, Field, ErrorMessage } from 'vee-validate';
    import * as yup from 'yup';
    import { ref } from 'vue';

    const typeSearchList = ['title', 'price'];

    const schema = yup.object({
        title:      yup.string(),
        price:      yup.number().typeError('Должно быть числом'),
        typeSearch: yup.string().oneOf(typeSearchList, 'По какому полю искать?').required('Страна обязательна*'),
    });

    const catalogItemSearch = defineModel('searchData');
    const typeSearchModel = ref('title');

    const emit = defineEmits(['searchItem']);
    function onSearch(values){
        emit('searchItem', values);
    }

    function clearValue(){
        switch(typeSearchModel.value){
            case "title":
                catalogItemSearch.value = '';
                break;
            case 'price':
                catalogItemSearch.value = '0';
                break;
        }
    }
</script>

<template>
    <div class="search__block">
        <Form @submit="onSearch" :validation-schema="schema">
            <label for=""> Выберите по какому фильтру искать
                <Field
                    name="typeSearch"
                    as="select"
                    v-model="typeSearchModel"
                    @input="clearValue"
                >
                    <option value="title">Название товара</option>
                    <option value="price">Цена товара</option>                 
                </Field>
            </label>
            <label><Field :name="typeSearchModel" type="text" v-model="catalogItemSearch"/><ErrorMessage :name="typeSearchModel"/></label>
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