<template>
    <div class="catalog__list-item">
        <a :href="'#' + item.id" class="item" @click="chooseItem">
            <div class="item-image">
                <img :src="item.image" alt="">
            </div>
            <div class="item-main__info">
                <div class="item-title">
                    <div href="">{{ item.title }}</div>
                </div>
                <div class="item-price">
                    <span>price: {{ item.price }}</span>
                </div>
            </div>
        </a>
        <div class="uplaud__item" @click="updateItem">Редактировать элемент</div>
    </div>
</template>

<script setup>
    defineProps(["item"]);

    const emit = defineEmits(['chooseItem', 'updateItem']);

    function chooseItem(){
        emit("chooseItem");
    }

    function updateItem(item){
        emit('updateItem');
    }
</script>

<style scoped>
    .catalog__list-item{
        border: 2px solid #ffffff0a;
    }
    a{
        color: #fff;
    }
    .item{
        padding: 10px;
        border-radius: 4px;
        background-color: #ffffff00;
        transition: background-color .5s;
        height: 400px;
        display: flex;
        flex-direction: column;
        cursor: pointer;
    }

    .item:hover{
        background-color: #ffffff0a;
    }

    .item-title div{
        color: #fff;
    }

    .item-image{
        height: 250px;
        display: flex;
        justify-content: center;
        align-items: center;
        flex: 0 1 250px
    }

    .item-image img{
        width: auto;
        max-width: 50%;
        max-height: 60%;
        height: auto;
        display: block;
    }

    .item-main__info{
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        flex: 1 1 auto
    }
    .uplaud__item{
        position: relative;
        padding: 10px;
        text-align: center;
        z-index: 1000;
        cursor: pointer;
        transition: background-color .5s;
    }

    .uplaud__item:hover{
        background-color: #ffffff0a;
    }
</style>