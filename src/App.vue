<template>
  <header>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" referrerpolicy="no-referrer" />
  </header>
  <h1>Reddit Random</h1>
  <ProgressBar/>
  <Image @reload="getPost" :url="imageUrl" /><br>
  <div class="wrapper">
    <div class="settings">
    <TypeSelector @toggle-type="toggleType" :activeTypes="activeTypes" />
    <TagSelector @new-tag="newTag" @delete-tag="deleteTag" :tags="activeTags" />
    </div>
    <div class="saveslots">
      <SaveSlots @save="saveSlot" @load-slot="loadSlot" @delete-slot="deleteSlot" :slots="slots" />
    </div>
  </div>
  
</template>

<script>
import Image from "./components/Image"
import TagSelector from "./components/TagSelector"
import TypeSelector from "./components/TypeSelector"
import SaveSlots from "./components/SaveSlots"
import ProgressBar from "./components/ProgressBar"
import {reddit} from "reddit.images"

export default {
  name: 'App',
  components: {
    Image,
    TagSelector,
    TypeSelector,
    SaveSlots,
    ProgressBar,
  },
  methods: {
    async getPost(){
      var subreddit = this.activeTags[Math.floor(this.random(1,this.activeTags.length+1)-1)];
      var type = this.activeTypes[Math.floor(this.random(1,this.activeTypes.length+1)-1)];
      reddit.FetchSubredditPost(subreddit, type).then((post) => {
        if(post.image.toLowerCase().endsWith("png") || post.image.toLowerCase().endsWith("jpg") || post.image.toLowerCase().endsWith("gif")){
          this.imageUrl = post.image;
          this.currentImage.image = post.image;
          this.currentImage.id = post.title;
          this.currentImage.nsfw = post.NSFW;
        }
        else{
          this.imageUrl = "https://community.spotify.com/t5/image/serverpage/image-id/106208i2C0401950E6463A4/image-size/medium?v=v2&px=400";
        }
        //console.log(post.image);
      });
    },
    deleteTag(tag){
      var index = this.activeTags.indexOf(tag);
      this.activeTags.splice(index, 1);
    },
    newTag(tag){
      this.activeTags.push(tag);
    },
    random(mn, mx) { 
      return Math.random() * (mx - mn) + mn;
    },
    toggleType(type){
      
      if(this.activeTypes.includes(type)){
        var index = this.activeTypes.indexOf(type);
        this.activeTypes.splice(index, 1);
      }
      else{
        
        this.activeTypes.push(type);
      }
    },
    loadSlot(id){
      var loadSlot = [...this.slots].filter(slot => slot.id == id);
      console.log(loadSlot);
      this.imageUrl = loadSlot[0].image;
    },
    saveSlot(){
      console.log("hello");
      this.currentImage.id = this.truncateString(this.currentImage.id, 20);
      this.slots.push({...this.currentImage});
    },
    deleteSlot(id){
      var deleteSlot = [...this.slots].filter(slot => slot.id == id);
      this.slots.splice(deleteSlot, 1);
    },
    truncateString(str, num){
      if(str.length <= num){
        return str;
      }
      return str.substring(0, num) + "...";
    }
  },
  data(){
    return {
      imageUrl: String,
      currentImage: {
        id: "Click here to start",
        image: "https://www.tynker.com/projects/images/5b3a43e976f293bc448b456a/click-here-to-start-button---click-here-to-start-button.png",
        nsfw: false,
      },
      activeTags: ["unixporn", "memes"],
      activeTypes: ["hot", "rising"],
      slots: [],
    }
  },
  created(){
    this.imageUrl = "https://www.tynker.com/projects/images/5b3a43e976f293bc448b456a/click-here-to-start-button---click-here-to-start-button.png";
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #F0F7EE;
  background-color: #4D556A;
  border-radius: 5px;
}
body{
  background-color: #454C5F;
}
.wrapper{
  display: flex;
  justify-content: center;
  align-content: center;
}
.settings{
  margin-right: 10px;
}
</style>
