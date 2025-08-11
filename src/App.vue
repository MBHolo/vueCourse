<script setup>
  import { ref } from 'vue';

  const usersList = ref([
    { 
      userInfoName: 'Иван',
      userPhone: "+79004445234",
    },
    { 
      userInfoName: 'Максим',
      userPhone: "+79225662333",
    },
    { 
      userInfoName: 'Мария',
      userPhone: "+79512324413",
    },
    { 
      userInfoName: 'Александр',
      userPhone: "+79111111111",
    },
  ]);

  const show = ref(false);
  const showAll = ref(false);
  const active = "active";
  const showElem = ref();
  const backgraoundColorItem = "#686767";

  function showInfo(i){
    showElem.value = i;
    showAll.value = false;
  }

  function showAllInfo(){
    showAll.value = !showAll.value;
  }

</script>

<template>

  <div v-for="(user, i) in usersList" class="users__item">
    <div @click="showInfo(i)" :class="['user__info-name', { active: showElem == i}]">
      {{ user.userInfoName }}
    </div>
    <div v-if="showElem == i || showAll" class="user__info-phone">
      {{ user.userPhone }}
    </div>
  </div>

  <button @click="showAllInfo">Показать все</button>

</template>

<style scoped>
  .users__item{
    margin-bottom: 5px;
  }

  .user__info-name{
    padding: 10px;
    background-color: #313131;
    min-width: 200px;
    transition: background-color .5s;
    cursor: pointer;
  }

  .user__info-name.active{
    background-color: #686767;
  }

  .user__info-name:hover{
    background-color: v-bind("backgraoundColorItem");
  }

  .user__info-phone{
    margin: 10px;
    height: 40px;
    transition: height .5s;
  }
</style>
