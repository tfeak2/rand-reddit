<template>
    <form @submit="onSubmit">
        <input v-model="newTagName" placeholder="add subreddit" type="text">
        <input class="submit" type="submit" value="submit">
    </form>
    <div class="tags" v-for="tag in tags" :key="tag">
        <div class="tag"><div class="text">{{tag}}</div><i @click="$emit('delete-tag', tag)" class="fas fa-times"></i></div>
    </div>
</template>
<script>
export default {
    name: "TagSelector",
    props: {
        tags: Array,
    },
    data(){
        return {
            newTagName: "",
        }
    },
    methods: {
        onSubmit(e){
            e.preventDefault();
            this.$emit("new-tag", this.newTagName);
            this.newTagName = "";
        }
    }
}
</script>
<style scoped>
    form{
        margin-bottom: 2px;
    }
    .tag{
        display: flex;
        background-color: #565E76;
        width: 200px;
        padding: 0px 2px;
        border-radius: none;
        width: 200px;
        margin-bottom: 2px;
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
    .submit{
        width: 50px;
        
        background-color: #5FB0FC;
        color: #F0F7EE;
        cursor: pointer;
    }
    .text{
        text-align: left;
        width: 170px;
    }
</style>