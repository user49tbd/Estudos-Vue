<template>
  <div class="ContainerMain">
    <BannerVue :btn="changeVal" :title="'Burger Maker'"/>
    <BurgerFormVue @change-v="changeVal()" :vis="visi"/>
  </div>
</template>

<script>
import BannerVue from '../components/Banner.vue'
import BurgerFormVue from '../components/BurgerForm.vue'
export default {
  name: 'HomeView',
  data(){
    return{
      visi:false
    }
  },
  methods:{
    changeVal(){
      this.visi = !this.visi
    }
  },
  components:{
    BannerVue,
    BurgerFormVue
  },
  
}
</script>
<style scoped>
  .ContainerMain{
    min-height: 30vh;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    flex-direction: column;
  }
  .ContainerMain > p:nth-of-type(1){
    font-size: 45px;
    text-align: center;
    font-weight: bolder;
    text-transform: uppercase;
  }
</style>