<template>
  <div class="burger-table">
    <table v-if="dataOrder.length > 0">
      <thead>
        <tr>
          <th>Cliente</th>
          <th>Pão</th>
          <th>Carne</th>
          <th>Opcionais</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="res in dataOrder" :key="res.id">
          <td>{{ res.name }}</td>
          <td>{{ res.bread }}</td>
          <td>{{ res.meat }}</td>
          <td>
            <ul>
              <li v-for="(op, index) in res.optionals" :key="index">
                {{ op }}
              </li>
            </ul>
          </td>
          <td>
            <select name="status" class="status" v-on:change="updateItem($event,res.id)">
              <option
                v-for="s in status"
                :value="res.tipo"
                :key="s.id"
                :selected="res.status == s.tipo"
              >
                {{ s.tipo }}
              </option>
            </select>
            <button v-on:click="rmvItem(res.id)">Cancelar</button>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="msgP" v-if="!dataOrder.length > 0">
      <p>Nenhum Pedido Cadastrado</p>
    </div>
  </div>
</template>
<script>
import {gVals} from "../mainVals/data.js"
export default {
  name: "DashBoard",
  data() {
    return {
      dataOrder: [],
      status:[]
    };
  },
  setup(){
    return {gVals}
  },
  methods: {
    async getOrders() {
      try {
        let response = await fetch("http://localhost:3000/burgers", {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
          },
        });
        if (!response.ok) {
          throw new Error("erro ao Obter pedidos");
        }
        let data = await response.json();
        this.dataOrder = data
      } catch {
        console.log("error")
        this.showMsg("Erro ao obter pedidos",1)
      }
    },
    async getStatus() {
      try {
        let response = await fetch("http://localhost:3000/status", {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
          },
        });
        if (!response.ok) {
          throw new Error("erro ao Obter Status");
        }
        let data = await response.json();
        this.status = data
      } catch {
        console.log("error")
        this.showMsg("Erro ao obter Status",1)
      }
    },
    async rmvItem(id){
      try{
        let req = await fetch(`http://localhost:3000/burgers/${id}`,{
        method:"DELETE",
        headers:{
          "Content-Type": "application/json",
        }
      })
      if(!req.ok){
        throw new Error("erro ao deletar")
      }

      let data = await req.json()

      this.getOrders();

      this.showMsg("deletado com sucesso",2)

      }catch{
        this.showMsg("Erro ao deletar",1)
      }
    },
    async updateItem(event,id){
      let opt = event.target.value
      let dataJ = JSON.stringify({status:opt})
      try{
        let req = await fetch(`http://localhost:3000/burgers/${id}`,{
        method:"PATCH",
        headers:{
          "Content-Type": "application/json",
        },
        body:dataJ
      })
      if(!req.ok){
        throw new Error("erro ao autualizar status")
      }

      let data = await req.json()

      this.showMsg(`atualizado com sucesso para ${opt}`,2)

      }catch{
        this.showMsg("erro ao autualizar status",1)
      }
    },
    showMsg(msg,type){
      this.gVals.msg=msg
      this.gVals.vis=true
      this.gVals.type=type
    },
  },
  mounted() {
    this.getStatus()
    this.getOrders()
  },
};
</script>
<style scoped>
.burger-table {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 90%;
}

table,
tr,
th,
td,
thead,
tbody {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}
table,
thead,
tbody {
  flex-direction: column;
}
thead {
  height: 50px !important;
  background-color: black;
  color: white;
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
}
tbody {
  justify-content: flex-start !important;
  overflow-y: auto;
}
tbody > tr:nth-child(odd) {
  background-color: rgb(209, 209, 209);
}
tbody > tr:nth-child(even) {
  background-color: white;
}
tbody > tr:nth-last-child(1) {
  border-bottom-left-radius: 15px;
  border-bottom-right-radius: 15px;
}
tr {
  height: 100px !important;
}
tr > td {
  height: 100%;
}
table {
  align-items: flex-start !important;
  width: 100%;
  /*height: 100% !important;*/
  table-layout: fixed;
  overflow: hidden;
  margin-bottom: 20px;
}
tr > td:nth-of-type(5) {
  gap: 5px;
  padding: 7px;
}
tr > td:nth-of-type(5) > * {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
}
tr > td:nth-of-type(4) {
  justify-content: flex-start;
  font-size: 12px !important;
}
tr > td:nth-of-type(4) > * {
  margin-left: 40%;
  margin-right: auto;
}
tr > td:nth-of-type(5) > button {
  transition: 0.5s;
  text-transform: uppercase;
  font-weight: bolder;
  background-color: black;
  color: white;
}
tr > td:nth-of-type(5) > button:hover {
  background-color: white;
  color: black;
}
.msgP{
  display: flex;
  align-items: center;
  justify-content: center;
  width: 70%;
  font-size: 50px;
  text-transform: uppercase;
  font-weight: bolder;
  font-family: Arial;
  color: white;
  background-color: black;
  border-radius: 5px;
}
</style>