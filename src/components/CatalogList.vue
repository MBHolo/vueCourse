<template>
    <a :href="'#' + item.id" class="item" @click="chooseItem">
        <div class="item-image">
            <img :src="item.image" alt="">
        </div>
        <div class="item-main__info">
            <div class="item-title">
                <div href="">{{ item.title }}</div>
            </div>
            <div class="item-price">
                <span>{{ item.price }}</span>
            </div>
        </div>
    </a>
</template>

<script setup>
    defineProps(["item"]);

    const emit = defineEmits();

    function chooseItem(){
        emit("choose");

    }
</script>

<style scoped>
    a{
        color: #fff;
    }
    .item{
        padding: 10px;
        border: 1px solid #ffffff0a;
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
</style>