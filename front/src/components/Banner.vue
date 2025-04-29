<template>
  <div class="bkMain">
    <div class="Content">
      <p>www.example.com</p>
      <h1>{{ title }}</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptatem,
        odio quos facere repudiandae rem suscipit mollitia perspiciatis nostrum,
        officiis quae, eius illum voluptatum iure et nam similique natus
        voluptate sapiente?
      </p>
      <button v-on:click="btn()">make</button>
    </div>
    <div class="icon">
        <img src="/assets/icons/burger.png">
    </div>
  </div>
</template>
<script>
export default {
  name: "Banner",
  //props: ["title","btn"],
  props:{
    title:{
        type:String,
        required:true
    },
    btn:{
        type:Function,
        required:true
    }
  },
  data() {
    return {};
  },
};
</script>
<style scoped>
.bkMain {
  width: 100%;
  height: 80vh;
  background-image: url("/public/assets/imgs/burg.jpg");
  background-color: yellow;
  background-blend-mode: darken;
  background-position: 50% 80%;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  color: white;
  position: relative;
}
.Content{
    width: 25%;
    height: 70%;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    flex-direction: column;
    padding-left: 10px;
    margin-left: 10px;
    gap: 5px;
}
.Content > p:nth-of-type(1){
    font-size: 12px;
}
.Content > h1{
    font-size: 60px;
    text-transform: uppercase;
    font-weight: bolder;
    font-family: Arial;
    border-top: 2px solid white;
    margin-top: 5px;
    padding-top: 5px;
}
.Content > p{
    text-align: justify;
}
.Content > button{
    width: 50%;
    height: 30px;
    background-color: black;
    color: white;
    font-size: 25px;
    text-transform: uppercase;
    font-family: Arial;
    transition: 0.5s;
    border-radius: 5px;
}
.Content > button:hover{
    background-color: white;
    color: black;
}
.icon{
    position: absolute;
    right: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    aspect-ratio: 1/1;
}
.icon > img{
    width: 100%;
    aspect-ratio: 1/1;
    object-fit: cover;
    object-position: center;
    filter: invert(1);
}
</style>
