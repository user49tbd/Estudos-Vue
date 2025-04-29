<template>
  <div class="messageC" v-if="vis">
    <div class="Content">
      <img v-bind:src="truType" />
      <div class="msgData">
        <p>{{ msg }}</p>
      </div>
    </div>
    <img class="xicon" v-on:click="closeM()" src="/assets/imgs/x-button.png" />
  </div>
</template>
<script>
export default {
  name: "Message",
  props: {
    msg: {
      type: String,
      required: true,
    },
    vis: {
      type: Boolean,
      required: false,
    },
    type: {
      type: Number,
      required: true,
    },
  },
  watch: {
    vis(val) {
      if (val == true) {
        this.timer();
      }
    },
  },
  emits: ["close-emit"],
  data() {
    return {
      time: "",
    };
  },
  computed: {
    truType() {
      return this.checkType(this.type);
    },
  },
  methods: {
    closeM() {
      this.$emit("close-emit");
      clearTimeout(this.time);
      console.log("end timer");
    },
    checkType(res) {
      console.log("checking type" + this.type);
      switch (res) {
        case 1:
          return "/assets/icons/caution-sign.png";
        case 2:
          return "/assets/icons/check-mark_15761039.png";
      }
    },
    timer() {
      console.log("checking timer");
      this.time = setTimeout(() => {
        //this.reset()
        this.closeM();
      }, 3000);
    },
  },
  mounted() {
    this.checkType();
  },
};
</script>
<style scoped>
.messageC {
  width: 70%;
  height: 50px;
  border-radius: 5px;
  color: white;
  position: fixed;
  top: 5px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 5px;
  z-index: 10;
}
.xicon {
  position: absolute;
  top: 0px;
  right: 0px;
  margin: 10px;
  height: 20px;
  aspect-ratio: 1/1;
}
.Content {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black;
  border-radius: 5px;
  position: relative;
  padding: 5px;
}
@property --angle{
  syntax: "<angle>";
  initial-value:0deg;
  inherits:false
}
.Content::before{
  content: "";
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: white;
  width: 100%;
  height: 100%;
  padding: 5px;
  animation: animate 2s infinite linear;
  background-image: conic-gradient(from var(--angle),black 70%, white,black);
  z-index: -1;
  border-radius: 5px;
}
@keyframes animate {
    from{
      --angle:0deg;
    }to{
      --angle:360deg;
    }
}
.Content > img {
  object-fit: cover;
  object-position: center;
  height: 100%;
  aspect-ratio: 1/1;
  filter: invert(1);
}
.Content > .msgData {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding-left: 5px;
  font-weight: bolder;
  width: 100%;
  height: 100%;
}
</style>