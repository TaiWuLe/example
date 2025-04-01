<template>
  <div style="margin-bottom: 20px;background-color: aqua;font-size: 20px; font-weight: bold">
    主页
  </div>
  <div style="font-size: 30px;margin-bottom: 20px;">
    {{ a }} {{b}}
  </div>
  <div style="margin-bottom: 20px;">
    {{data.a}}
    {{data.b}}
  </div>
  <div style="margin-bottom: 20px;">
    <input v-model="data.name" style="margin-right: 10px"/>
    <input v-model="data.arr" style="margin-right: 10px"/>
    <input v-model="test.food" style="margin-right: 10px"/>
  </div>
  <div style="margin-bottom: 20px;">
    <span style="color: red" v-if="data.name == '佩奇'">小猪佩奇</span>
    <span style="color: blue;" v-else-if="data.name == '乔治'" >小猪乔治</span>
    <span style="color: hotpink;" v-else >小猪朵朵</span>
  </div>
  <div style="display: flex;margin-bottom: 10px">
    <div @click="show(item)" v-for="item in data.arr" style="width: 300px;height: 300px;background-color: green; text-align: center;line-height: 300px;font-size: 30px; margin-right: 10px"> {{item}}</div>
    <div>
      <select style="width: 200px ;margin-bottom: 20px">
        <option v-for="fruit in data.fruits">{{ fruit }}</option>
      </select>
    </div>
  </div>

  <div style="margin-bottom: 10px">
    <button @click="click">点我送地狱火</button>
  </div>
  <div style="margin-bottom: 20px">
    <div :style="data.box"></div>
    <div><img :src=data.img alt=""></div>
  </div>
  <div style="margin-left: 20px;margin-bottom: 10px">
    <el-button @click="clickData" :style="{color : 'red'}">Default</el-button>
    <el-button type="primary" plain>Primary</el-button>
    <el-button type="success" round>Success</el-button>
    <el-button type="info" circle>Info</el-button>
    <el-button type="warning" loading>Warning</el-button>
    <el-button type="danger" color="yellow">Danger</el-button>
  </div>
  <div style="margin-left: 30px">
    <el-icon :size="30">
      <Edit />
    </el-icon>
    <span style="margin-left: 20px">
      <el-icon size="30px" >
      <Aim />
    </el-icon>
    </span>
    <span style="margin-left: 20px; color: blue">
      <el-icon size="20px" color="red" style="top: 4px ">
      <View />
    </el-icon> 100
      <el-button :icon="Search" circle />
      <el-button type="primary" :icon="Edit" circle />
      <el-button type="success" :icon="Check" circle />
      <el-button type="info" :icon="Message" circle />
      <el-button type="warning" :icon="Star" circle />
      <el-button type="danger" :icon="Delete" circle />
      <el-input
          v-model="data.name"
          style="width: 240px;margin-left: 10px"
          placeholder="Type something"
          :prefix-icon="Search"
      />



    </span>

  </div>


</template>



<script setup>

import {reactive, ref, onMounted} from "vue";
import {Check, Delete, Edit, Message, Search, Star} from "@element-plus/icons-vue";

const a = ref(1)
const b = ref("波波真的帅")

const data = reactive({
  a: 123,
  b: "波波真的帅帅的",
  name:'佩奇',
  arr: [1,2,3],
  fruits: ["苹果","香蕉","哈密瓜","水蜜桃","榴莲"],
  box:{
    width: "100px",
    height: "100px",
    backgroundColor: "red"
  },
  img: "https://www.runoob.com/wp-content/uploads/2017/01/vue.png",

})

onMounted(() =>{
  console.log("页面加载完成")
})
const test = reactive({
  food: ["米饭","面条","饺子"],

})
const clickData = () => {
  alert("点击事件")
}
const click = () =>{
  alert("你获得地狱火了")
}

const show = (value) =>{
  alert(value)
}
</script>