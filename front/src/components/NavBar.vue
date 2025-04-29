<template>
  <nav>
    <router-link to="/"><div class="mainR"><img v-bind:src="imgLogo" id="logo" /><p>Burg<br><span>Master</span></p></div></router-link>
    <router-link to="/">Home</router-link>
    <router-link to="/pedido">Pedidos</router-link>
  </nav>
</template>
<script>
export default{
    name:"NavBar",
    props:{
        imgLogo:{
            type:String,
            required:true
        }
    },
    //props:["val","alt"]
    data(){
        return{

        }
    }
}
</script>
<style scoped>
nav{
    width: 100%;
    height: 20vh;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    gap: 5px;
    padding: 5px;
    background-color: black;
}
nav >*{
    text-decoration: none;
    color: white;
}
nav >*:nth-child(1){
    display: flex;
    align-items: flex-start;
    justify-content: flex-start;
    margin-left: 0px;
    margin-right: auto;
    height: 100%;
}
nav a{
    font-size: 20px;
    transition: 0.5s;
}
nav a:not(:nth-child(1)):hover{
    color: orange;
}
.mainR{
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    gap: 10px;
    padding: 5px;
    line-height: 25px;
}
.mainR > img{
    height: 100%;
    aspect-ratio: 1/1;
    object-fit: cover;
    object-position: center;
    filter: invert(1);
}
.mainR p,.mainR span{
    font-size: 60px;
    text-transform: uppercase;
    font-weight: bolder;
}
.mainR span{
    font-size: 30px !important;
    color: orange;
}
</style>
