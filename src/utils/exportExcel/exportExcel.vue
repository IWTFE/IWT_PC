<!--列表-->
<template>
  <div class="inline-display">
    <el-button v-on:click="excel">导出</el-button>
    <div v-show="isExport">
      <table :id="tableId">
        <tr v-for="(tr, index) in listData">
          <td v-if="index === 0" v-for="td in tr.title">{{td}}</td>
          <td v-if="index !=0" v-for="td in tr">{{td}}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script type="text/javascript">
  import expTool from './export.js'
  export default{
    data: function(){
      return {
        isExport: false,
        tableId: "exportExcel"
      }
    },
    props: ['listData'],
    methods: {
      excel: function(){
        expTool.getExcel(this.tableId);
      }
    }
  }
</script>
<style media="screen">
  .inline-display{display: inline-block}
</style>
