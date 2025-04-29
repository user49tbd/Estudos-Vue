<template>
  <div>
  <NavBarVue :imgLogo="'/assets/icons/burger.png'"/>
  <router-view/>
  <FooterVue/>
  <messageVue :vis="gVals.vis" :msg="gVals.msg" :type="gVals.type" @close-emit="changeVal()"/>
  </div>
</template>
<script>
import FooterVue from './components/Footer.vue';
import messageVue from './components/message.vue';
import NavBarVue from "./components/NavBar.vue";
import {gVals} from "./mainVals/data.js"
export default{
  components:{
    NavBarVue,
    FooterVue,
    messageVue
  },
  setup() {
    return { gVals }; // agora o template pode usar
  },
  methods:{
    changeVal(){
      this.gVals.vis = false
      this.gVals.msg = ""
      //this.visi = !this.visi
    }
  }
}
</script>

<style>
*{
  padding: 0px;
  border: 0px;
  margin: 0px;
  box-sizing: border-box;
}
</style>
