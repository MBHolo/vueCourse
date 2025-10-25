<script setup>
    import { reactive } from 'vue';
    import { ref } from 'vue';
    import CatalogList from './components/catalog/CatalogList.vue';
    import CatalogDetail from './components/catalog/CatalogDetail.vue';
    import HeaderPage from './components/pageLBlocks/HeaderPage.vue';
    import OrderForm from './components/forms/OrderForm.vue';
    import UpdateItem from './components/forms/UpdateItem.vue';

    //Подключение библиоотеки axios для загрузки извне данных
    import axios from 'axios';

    //Реактивный массив данных каталога
    const catalogItems = reactive([]);
    const loading = ref(false);
    const error = ref(null);

    loading.value = true;
    error.value = null;
    
    try {
        axios.get('https://fakestoreapi.com/products').then((response) => {
            catalogItems.splice(0, catalogItems.length, ...response.data);
        });
    } catch (err) {
        error.value = 'Ошибка при загрузке данных: ' + err.message;
    } finally {
        loading.value = false;
    }

    //Элемент каталога для показа
    const itemCatalogChoose = ref('');

    //Поиск элемента
    const itemCatalogSerarch = ref('');

    //Выбор элемента для редактирования
    const itemChooseUpdate = ref('');
    const titleItemUpdate = ref('');
    const priceItemUpdate = ref('');
    const idItemUpdate = ref('');

    const activeForm = ref('');

    //Функция выбора элемента для отображения
    function chooseItem(itemId){
        itemCatalogChoose.value = catalogItems.find((t) => t.id == itemId);
    }

    //Функция поиска
    function searchBlock(event){
        if(event.price){
            itemCatalogSerarch.value = event.price;
            itemCatalogChoose.value = catalogItems.find((t) => t.price == itemCatalogSerarch.value);
        } else {
            itemCatalogSerarch.value = event.title;
            console.log(event.title);
            itemCatalogChoose.value = catalogItems.find((t) => t.title == itemCatalogSerarch.value);
        }
    }

    //Функция отправки формы заказа
    function order(event){
        console.log(event);
    }

    //Функция обновления элемента
    function updateItemChoose(itemUpdate){
        itemChooseUpdate.value = itemUpdate;
        titleItemUpdate.value = itemChooseUpdate.value.title;
        priceItemUpdate.value = itemChooseUpdate.value.price;
        idItemUpdate.value = itemChooseUpdate.value.id;
        activeForm.value = "active";

    }

    function closeForm(){
        activeForm.value = "";
    }

    //Функция динамичного обновления элемента
    function updateItemSave(itemInfo){
        let updateItemFind = catalogItems.find((t) => t.id == itemInfo.idItemForm);
        updateItemFind.title = itemInfo.titleItemForm;
        updateItemFind.price = itemInfo.priceItemForm;
    }

</script>

<template>
    <div class="header">
        <HeaderPage @showSearchItem="searchBlock($event)"></HeaderPage>
    </div>
    <div class="items__detail">
        <CatalogDetail :itemChoose="itemCatalogChoose"></CatalogDetail>
    </div>
    <div class="items__list">
        <CatalogList v-for="item in catalogItems" :key="item.id" :item="item" @chooseItem="chooseItem(item.id)" @updateItem="updateItemChoose(item)"></CatalogList>
    </div>
    <div class="form__update" :class="activeForm">
        <h2>форма изменения элемента</h2>
        <span class="close__button" @click="closeForm">Закрыть</span>
        <UpdateItem v-model:itemTitle="titleItemUpdate" v-model:itemPrice="priceItemUpdate" v-model:itemId="idItemUpdate" @updateItemInfo="updateItemSave($event)"></UpdateItem>
    </div>
    <div class="order__form">
        <h2>Форма заказа</h2>
        <OrderForm @order="order($event)"></OrderForm>
    </div>
</template>

<style scoped>
    .header{
        width: 100%;
        height: 100px;
        margin-top: 20px;
        padding: 10px;
        border: 1px solid #ffffff0a;
        border-radius: 4px;
        margin-bottom: 20px;
    }
    .items__detail{
        height: 600px;
        width: 100%;
        border: 1px solid #ffffff0a;
        border-radius: 4px;
        background-color: #ffffff00;
        margin: 0px 0px 40px 0px;
    }
    .items__list{
        display: grid;
        grid-template-columns: repeat(4, 25%);
        gap: 20px;
        max-width: 100%;
    }
    .order__form{
        margin: 40px;
    }
    .form__update{
        max-width: 400px;
        padding: 40px;
        position: fixed;
        top: 200px;
        background-color: #1a1a1a;
        z-index: 10000;
        left: 50%;
        transform: translate(-50%);
        display: none;
    }

    .form__update.active{
        display: block;
    }
    .close__button{
        position: absolute;
        top: 10px;
        right: 20px;
        cursor: pointer;
    }
    
</style>