<template>
  <div class="ContainerBF" v-if="vis">
    <div class="sideF">
      <img src="/assets/icons/burger.png" />
      <p>form</p>
    </div>
    <form v-on:submit.prevent="subs()">
      <div class="Field">
        <label for="name">Nome</label>
        <input
          type="text"
          name="name"
          id="name"
          v-on:input="changeForm($event)"
          placeholder="Nome"
        />
      </div>
      <div class="Field">
        <label for="bread">Pao</label>
        <select name="bread" id="bread" v-on:input="changeForm($event)">
          <option value="">Selecione o seu pao</option>
          <option v-for="res in paes" :key="res.id" :value="res.tipo">
            {{ res.tipo }}
          </option>
        </select>
      </div>
      <div class="Field">
        <label for="meat">Carne</label>
        <select name="meat" id="meat" v-on:input="changeForm($event)">
          <option value="">Selecione o seu carne</option>
          <option v-for="res in carnes" :key="res.id" :value="res.tipo">
            {{ res.tipo }}
          </option>
        </select>
      </div>
      <div class="FieldCheck">
        <label for="opcionais">Selecione os Opcionais</label>
        <div class="checkBoxContainer" v-for="res in opcionais" :key="res.id">
          <input
            type="checkbox"
            name="optionals"
            :value="res.tipo"
            :id="res.id"
            v-on:change="changeForm($event)"
          />
          <span :for="res.id">{{ res.tipo }}</span>
        </div>
      </div>
      <div class="submitC">
        <input type="submit" value="Enviar" class="subs" />
      </div>
    </form>
    <img
      class="xicon"
      v-on:click="changeVal()"
      src="/assets/imgs/x-button.png"
    />
  </div>
</template>
<script>
import {gVals} from "../mainVals/data.js"
export default {
  name: "BurgerForm",
  props: {
    vis: {
      type: Boolean,
      required: true,
    },
  },
  setup() {
    return { gVals };
  },
  emits: ["changeV"],
  methods: {
    changeVal() {
      this.$emit("change-v");
    },
    subs() {
      console.log("submit");
      //this.showMsg("Pedido cadastrado",2)
      this.createBurg()
    },
    showMsg(msg,type){
      this.gVals.msg=msg
      this.gVals.vis=true
      this.gVals.type=type
    },
    changeForm(e) {
      let name = e.target.name;
      let val = e.target.value;
      console.log("this is the checked "+e.target.name)
      if (e.target.name == "optionals") {
        let arrI = this.formData[name]
        console.log("here is the arr of Items "+arrI)
        if (e.target.checked) {
          console.log("its checked")
          arrI.push(val)
          console.log("new arrI "+arrI)
        }else{
          console.log("its not checked")
          arrI = arrI.filter((res)=>res != val)
          console.log("new arrI "+arrI)
        }
        this.formData = { ...this.formData, [name]:arrI };
      } else {
        this.formData = { ...this.formData, [name]: val };
      }
    },
    async getIngredients() {
      try {
        let response = await fetch("http://localhost:3000/ingredientes", {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
          },
        });
        if (!response.ok) {
          throw new Error(`Erro na requisição: ${response.status}`);
        }

        let data = await response.json();
        console.log(data);

        this.paes = data.paes;
        this.carnes = data.carnes;
        this.opcionais = data.opcionais;
      } catch (error) {
        console.error("Erro ao buscar ingredientes:", error); // Trata erros
      }
    },
    async createBurg() {
      try {
        let response = await fetch("http://localhost:3000/burgers", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body:JSON.stringify(this.formData)
        });
        if (!response.ok) {
          throw new Error(`Erro na requisição: ${response.status}`);
        }
        let data = await response.json();
        console.log(data);
        this.formData= {name: "",bread: "",meat: "",optionals: [],status: "Solicitado"}

        this.showMsg(`Pedido Nº${data.id} realizado com sucesso`,2)
      
      } catch (error) {
        //console.error("Erro ao buscar ingredientes:", error); // Trata erros
        this.showMsg("Erro ao inserir dados",1)
      }
    },
  },
  data() {
    return {
      paes: "",
      carnes: "",
      opcionais: "",
      formData: {
        name: "",
        bread: "",
        meat: "",
        optionals: [],
        status: "Solicitado",
      },
    };
  },
  mounted() {
    this.getIngredients();
  },
};
</script>
<style scoped>
.ContainerBF {
  width: 70%;
  height: 70%;
  border-radius: 15px;
  box-shadow: 0px 5px 10px 0px rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: white;
  overflow: hidden;
}
.xicon {
  position: absolute;
  top: 0px;
  right: 0px;
  margin: 10px;
  height: 20px;
  aspect-ratio: 1/1;
  object-fit: cover;
  object-position: center;
}
.sideF {
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 20%;
  height: 100%;
  background-image: url("/public/assets/imgs/burg.jpg");
  background-color: yellow;
  background-blend-mode: darken;
  background-position: center;
  background-size: cover;
  padding: 5px;
}
.sideF > * {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.sideF > img {
  width: 100%;
  aspect-ratio: 1/1;
  object-fit: contain;
  object-position: center;
  filter: invert(1);
}
.sideF > p {
  text-orientation: upright;
  writing-mode: vertical-lr;
  text-transform: uppercase;
  font-weight: bolder;
  color: white;
  font-size: 30px;
}
form {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 20px;
}
.Field {
  display: flex;
  flex-direction: column;
  width: 100%;
  margin-bottom: 10px;
}
.Field > * {
  width: 100%;
}
label {
  margin-bottom: 5px;
  font-weight: bolder;
  text-transform: capitalize;
  padding-left: 5px;
  border-left: 4px solid orange;
}
.FieldCheck {
  display: flex;
  flex-direction: row !important;
  width: 100%;
  flex-wrap: wrap;
}
.FieldCheck > label {
  width: 100%;
}
.checkBoxContainer {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  width: 50%;
  margin-bottom: 10px;
  gap: 5px;
}
.submitC {
  width: 100%;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.submitC > input {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 5px;
  color: white;
  background-color: black;
  transition: 0.5s;
  font-size: 25px;
}
.submitC > input:hover {
  background-color: white;
  border: 1px solid black;
  color: black;
}
</style>