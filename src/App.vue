<script setup>
import groupData from "./assets/data.json";
import {onMounted, ref } from "vue";

import Button from "./components/Button/Button.vue";
import Card from "./components/Card/Card.vue";

const groupNames = ref([]);
const students = ref([]);
const selectedGroupName = ref('');

function getGroupNames() {
const groupNames = groupData.map(person => person.group);
const uniqueNames = [...new Set(groupNames)];
return uniqueNames;
}

const getStudents = (name) => {
  let  filterByGroupName = groupData.filter(person => person.group === name);
  return filterByGroupName;
}

const filterByNameHandler = (name) => {
  const result = getStudents(name);
  selectedGroupName.value = name;
  students.value = result; //neden resulta atıp geri kendisine eşitledik - okunaklı olması için mi?
  //return neden kullanmadık?
}

onMounted(() => {
  groupNames.value = getGroupNames();
})

</script>

<template>
  <main class="main">
    <header class="header">
      <Button v-for="name in groupNames" :key="name" :name="name" @setName="filterByNameHandler"></Button>
    </header>
    <div class="wrapper" :class="selectedGroupName">
      <Card v-if="students.length > 0" :data="students"></Card>
    </div>
  </main>
</template>

<style scoped>

  .main{
    width: 100%;
    min-height: 100vh;

    display: flex;
    flex-direction: column;
    align-items: stretch;

    justify-content: flex-start;
    background-color: bisque;
  }
  .header{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;

    min-height: 80px;

    background-color: pink;
  }
  .wrapper{
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;

    background-color: yellowgreen;
  }

</style>
