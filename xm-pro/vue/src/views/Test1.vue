<template>
  <div>
    <div style="margin-top: 10px;margin-left: 10px; margin-bottom: 20px">
      <el-input v-model="data.input" style="width: 240px" placeholder="Please input" :prefix-icon="Search"/> {{ data.input}}
      <el-input suffix-icon="Calendar" style="width: 240px;"/>
      <el-input type="textarea" v-model="data.desc" style="width: 300px" placeholder="一段描述"></el-input>
    </div>

    <div>
      <el-select
          multiple
          value-id="id"
          v-model="data.value"
          placeholder="Select"
          size="large"
          style="width: 240px"
      >
        <el-option
            v-for="item in data.options"
            :key="item.id"
            :label="item.label"
            :value="item.name"
        />
      </el-select>{{data.value}}
    </div>
    <div style="margin: 10px">
      <el-radio-group v-model="data.sex">
        <el-radio value="男">男</el-radio>
        <el-radio value="女">女</el-radio>
      </el-radio-group>
      {{data.sex}}

      <el-radio-group style="margin-left: 20px" v-model="data.tag">
        <el-radio-button label="New York" value="New York" />
        <el-radio-button label="Washington" value="Washington" />
        <el-radio-button label="Los Angeles" value="Los Angeles" />
      </el-radio-group>
    </div>

    <div style="margin-left: 20px;margin-bottom: 10px">
      <el-checkbox-group v-model="data.list">
        <el-checkbox v-for="item in data.options" :key="item.id" :value="item.name" :label="item.label"  />
      </el-checkbox-group>
      <span style="margin-left: 20px">{{data.list}}</span>
    </div>
    <div stlye="margin-bottom: 10px">
      <el-image :src="img" style="width: 100px" :preview-src-list="[img]"/>
    </div>
    <div style="margin-bottom: 10px">
      <el-carousel height="800px" style="width: 500px">
        <el-carousel-item v-for="item in data.imgs" :key="item">
          <img :src="item" style="width: 100%;">
        </el-carousel-item>
      </el-carousel>
    </div>
    <div style="margin-bottom: 20px">
      <el-date-picker
          v-model="data.date"
          type="date"
          placeholder="Pick a day"
          :size="size"
          format="YYYY-MM-DD"
          value-format="YYYY-MM-DD"
      /> {{data.date}}

      <el-date-picker
          style="margin-left: 50px"
          v-model="data.date1"
          type="datetime"
          placeholder="Pick a day"
          :size="size"
          format="YYYY-MM-DD HH:mm:ss"
          value-format="YYYY-MM-DD HH:mm:ss"
      />{{data.date1}}

      <el-date-picker
          v-model="data.daterange"
          type="datetimerange"
          start-placeholder="Start Date"
          end-placeholder="End Date"
          format="YYYY-MM-DD"
          value-format="YYYY-MM-DD"
      /> {{data.daterange?.length ? data.daterange[0] : ''}} {{data.daterange?.length ? data.daterange[1] : ''}}
    </div>
    <div style="margin: 20px">
      <el-table :data="data.tableData" style="width: 100%" stripe>
        <el-table-column prop="date" label="日期" width="180" header-align="center"/>
        <el-table-column prop="name" label="姓名" width="180" />
        <el-table-column prop="address" label="地址 " />
        <el-table-column label="操作">
          <template #default="scope" >
            <el-button type="primary" @click="edit(scope.row)">
              <el-icon><Edit/></el-icon>
            </el-button>
            <el-button type="danger" @click="del(scope.row.id)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div style="padding: 10px 0">
        <el-pagination
            v-model:current-page="data.currentPage"
            v-model:page-size="data.pageSize"
            :page-sizes="[5, 10, 15, 20]"
            layout="total, sizes, prev, pager, next, jumper"
            :total="data.tableData.length"
        />
      </div>
    </div>
    <el-dialog v-model="data.dialogVisible" title="编辑行对象" width="500">
      <div style="padding: 20px">
        <div style="margin-bottom: 10px">{{data.row.date}}</div>
        <div style="margin-bottom: 10px">{{data.row.name}}</div>
        <div>{{data.row.address}}</div>
      </div>
    </el-dialog >

  </div>
</template>

<script setup>
import {reactive} from "vue";
import {Search,Edit,Calendar} from "@element-plus/icons-vue"
import img from '@/assets/logo.svg'


const data = reactive({
  input: null,
  desc: null,
  value: "null",
  options: [{id: 1 ,label: "苹果" , name: "苹果"},{id: 2,label: "香蕉" ,name: "香蕉"},{id: 3,label: "西瓜" ,name: "西瓜"},{id: 4 ,label: "苹果" , name: "红苹果"}],
  sex: null,
  tag: null,
  list: [],
  imgs: ["https://img0.baidu.com/it/u=4113193887,2232603936&fm=253&fmt=auto&app=138&f=JPEG?w=800&h=1776",
    "https://img0.baidu.com/it/u=646878687,2098717759&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=667",
    "https://img2.baidu.com/it/u=2163714613,300402842&fm=253&fmt=auto&app=120&f=JPEG?w=751&h=500"],
  date: '',
  date1: '',
  daterange: null,
  tableData: [
    {id:1, date: '2025-4-1' , name: 'bobo' ,address: '福建泉州'},
    {id:2, date: '2025-4-2' , name: 'boboj' ,address: '福建泉州'},
    {id:3, date: '2025-4-3' , name: 'boboy' ,address: '福建泉州'},
    {id:4, date: '2025-4-4' , name: 'boboe' ,address: '福建泉州'}
  ],
  currentPage: 1,
  pageSize: 5,
  dialogVisible: false,
  row: null,
})
const del = (id) =>{
  alert("删除id=" + id + "的数据")
}

const edit = (row) =>{
  data.row = row
  data.dialogVisible = true
}

</script>



