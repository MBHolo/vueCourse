<template>
    <div v-if="!itemChoose"class="item__choose-enemy">Choose item</div>
    <div v-else class="item__choose-choose" :id="itemChoose.id">
        <div class="item__choose-left__block">
            <div class="item__choose-image">
                <img :src="itemChoose.image" alt="">
            </div>
        </div>
        <div class="item__choose-right__block">
            <div class="item__choose-main__info">
                <div class="main__info-rating__stars">
                    <div class="star"></div>
                </div>
                <h1 class="main__info-title">{{ itemChoose.title }}</h1>
                <div class="main__info-price">Price: {{ itemChoose.price }}</div>
                <div class="main__info-description">{{ itemChoose.description }}</div>
            </div>
        </div>
    </div>
</template>

<script setup>
    defineProps(["itemChoose"]);
</script>

<style scoped>
    .item__choose-enemy{
        display: flex;
        flex-direction: column;
        justify-content: center;
        height: 100%;
        align-items: center;
        font-size: 40px;
        font-weight: 700;
    }
    .item__choose-choose{
        display: flex;
        height: 100%;
        width: 100%;
        padding: 20px;
    }
    .item__choose-left__block{
        width: 50%;
        padding: 20px;
        border-radius: 4px;
        border: 1px solid #ffffff0a;
    }
    .item__choose-right__block{
        width: 50%;
        padding: 20px;
    }  
    .main__info-title{
        font-size: 20px 
    }
    .main__info-description{
        margin-top: 20px;
    }
</style>