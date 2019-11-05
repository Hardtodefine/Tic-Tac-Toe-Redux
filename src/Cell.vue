<template>
  <div id="Cell" v-on:click="onClickSelf">
      <template v-if="a">
        <div v-show="false">{{text}}</div>
        <template v-if="text=='x'"><img width="105px" src="./image/cha.png" alt=""></template>
        <template v-else-if="text=='o'"><img width="105px" src="./image/yuan.png" alt=""></template>
      </template>
      <template v-else></template>
  </div>
</template>
<script>
export default {
  props:["n"],
  data(){
    return { a:false,text:null}
  },
  methods:{
    onClickSelf(){
    if(this.text!==null){
        return
    }
    this.a=true;
    this.text = this.n % 2 === 0 ? "x" : "o";
    this.$emit("click",this.text);
    }
  },
};
</script>
<style>
#Cell{
  border: 1px solid rgb(35, 72, 142);
  width: 100px;
  height: 100px;
}
</style>