<script setup>
    const props = defineProps(['item']);
</script>

<template>
    <li class="card__item" :class="{'assistant' : props.item.name }">{{props.item.name}}</li>
</template>

<style scoped>
.card__item {
    margin: 10px 0;
    background-color: teal;
}
.card__item.assistant {
    background-color: purple;
    color: aliceblue;
    order: -1;
}
</style>