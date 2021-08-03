<template>
    <button @click="$emit('toggle-type', 'hot')" :id="activeTypes.includes('hot')">Hot</button>
    <button @click="$emit('toggle-type', 'top')" :id="activeTypes.includes('top')">Top</button>
    <button @click="$emit('toggle-type', 'rising')" :id="activeTypes.includes('rising')">Rising</button>
    <button @click="$emit('toggle-type', 'new')" :id="activeTypes.includes('new')">New</button>
</template>
<script>
export default {
    name: "TypeSelector",
    props: {
        activeTypes: Array,
    }
}
</script>
<style scoped>
    button{
        border: none;
        border-radius: none;
        margin-bottom: 5px;
        background-color: #565E76;
        color: #F0F7EE;
        cursor: pointer;
        width: 50px;
        height: 25px;
    }
    #true{
        background-color: #5FB0FC;
    }
</style>