<template>
  <el-button v-on:click="printer()">打印</el-button>
</template>
<script type="text/javascript">
  export default { 
    props:["listID"],
    methods:{
      printer(){
        var iframe = document.createElement("iframe");
				var table = document.getElementById(this.listID).cloneNode(true);
				iframe.name = "frame";
				document.body.appendChild(iframe);
				var o = window.open("about:blank","frame");
				iframe.contentWindow.document.body.appendChild(table);
				iframe.contentWindow.print();
      }
    }
  }
</script>
