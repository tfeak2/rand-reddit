<template>
    <button class="save" @click="$emit('save')"><i class="fas fa-save"></i></button>
    <div v-for="slot in slots" :key="slot.id">
        <div class="slot" @click="$emit('load-slot', slot.id)"><div class="text">{{slot.id}}</div><i @click="$emit('delete-slot', slot.id)" class="fas fa-times"></i></div>
    </div>
</template>
<script>
export default {
    name: "SaveSlots",
    props: {
        slots: Array,
    }
}
</script>
<style scoped>
    .slot{
        display: flex;
        background-color: #565E76;
        width: 200px;
        padding: 0px 2px;
        border-radius: none;
        width: 200px;
        margin-bottom: 2px;
        cursor: pointer;
    }
    i{
        margin-left: 10px;
        cursor: pointer;
        text-align: left;
    }
    input{
        border: none;
        width: 147px;
        margin-right: 3px;
        border-radius: none;
        
    }
    .save{
        width: 50px;
        
        background-color: #5FB0FC;
        color: #F0F7EE;
        cursor: pointer;
        border: none;
    }
    .text{
        text-align: left;
        width: 170px;
    }
</style>