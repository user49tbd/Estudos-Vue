<template>
    <div class="ContainerMain">
      <p>Pedidos</p>
      <DashBoardVue/>
    </div>
</template>
<script>
import DashBoardVue from '../components/DashBoard.vue';
export default {
  name:"Pedidos",
  components:{
    DashBoardVue
  }
};
</script>
<style scoped>
.ContainerMain {
  min-height: 30vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-direction: column;
  position: relative;
}
.ContainerMain > p:nth-of-type(1) {
  font-size: 45px;
  text-align: center;
  font-weight: bolder;
  text-transform: uppercase;
}
</style>

