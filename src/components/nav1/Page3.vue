<template>
	<div>
	<el-tabs style="width:100%;" type="card" @tab-click="handleClick" @tab-remove="handleRemove">
		<el-tab-pane label="用户管理">
			<el-form ref="form" :model="form" label-position="center" label-width="100px" @submit.prevent="onSubmit" style="margin:10px;min-width:600px;">
					<el-row :gutter="40">
						<el-col :span="8">
							<el-form-item label="角色名称:">
								<el-select v-model="form.roleName">
									<el-option label="全部" value="" selected></el-option>
									<el-option v-for="item in roleName" :label="item" :value="item"></el-option>
								</el-select>
							</el-form-item>
						</el-col>
						<el-col :span="4">&nbsp;</el-col>
						<el-col :span="8">
							<el-form-item label="角色级别:">
								<el-select v-model="form.roleLevel">
									<el-option label="全部" value="" selected></el-option>
									<el-option v-for="item in roleLevel" :label="item" :value="item"></el-option>
								</el-select>
							</el-form-item>
						</el-col>
					</el-row>
					<el-row :gutter="40">
						<el-col :span="8">
							<el-form-item label="状态:">
								<el-select v-model="form.statu">
									<el-option label="全部" value="" selected></el-option>
									<el-option v-for="item in status" :label="item" :value="item"></el-option>
								</el-select>
							</el-form-item>
						</el-col>
						<el-col :span="4">&nbsp;</el-col>
						<el-col :span="8" style="text-align:right">
							<el-form-item>
								<el-button type="primary" @click="query">查询</el-button>
							</el-form-item>
						</el-col>
					</el-row>
			</el-form>
			<el-table :data="data" highlight-current-row v-loading="listLoading" style="margin:0 20px; width:auto; " id="table">
				<el-table-column type="index" width="70" label="序号"></el-table-column>
				<el-table-column prop="roleCode" label="角色代码" width="120" sortable>
				</el-table-column>
				<el-table-column prop="roleName" label="角色名称" width="140" >
				</el-table-column>
				<el-table-column prop="roleLevel" label="角色级别" width="100" >
				</el-table-column>
				<el-table-column prop="roleDescribe" label="角色描述" width="140">
				</el-table-column>
				<el-table-column prop="time" label="最后修改时间" sortable width="170"></el-table-column>
				<el-table-column prop="lastModified" label="最后修改人" width="160"></el-table-column>
				<el-table-column prop="statu" label="状态" width="80"></el-table-column>
				<el-table-column prop="remarks" label="备注" min-width="140"></el-table-column>
				<el-table-column inline-template :context="_self" label="操作" width="160">
					<span>
						<a @click="open(row)" style="color:blue; text-decoration:underline; cursor:pointer;">查看角色功能</a>
					</span>
				</el-table-column>
			</el-table>
		</el-tab-pane>
		<el-tab-pane label="打印">
			<el-row :gutter="80">
					<el-col :span="20" style="text-align:right">
						<el-print :target="'print'">打印本页内容</el-print>
					</el-col>
			</el-row>

		  <div id="print">
		      <h1 class="title">中国福利彩票积分服务</h1>
		      <h1 class="title"><span class="undeline">浙江省</span>省级积分服务月账单</h1>
		      <table border="0" cellspacing="0" cellpadding="8" align="center" class="head_info">
		        <tbody><tr>
		          <td class="bold" width="150">客户编号：</td>
		          <td width="150"></td>
		          <td width="150" class="bold">客户名称：</td>
		          <td width="100"></td>
		        </tr>
		        <tr>
		          <td class="bold">客户地址：</td>
		          <td></td>
		          <td class="bold">客户邮编：</td>
		          <td></td>
		        </tr>
		        <tr>
		          <td class="bold">总金额（小写）：</td>
		          <td>￥1236333.46</td>
		          <td class="bold">账期：</td>
		          <td>2016年9月</td>
		        </tr>
		        <tr>
		          <td class="bold">总金额（大写）：</td>
		          <td colspan="3">人民币壹佰贰拾叁万陆仟叁佰叁拾叁元肆角陆分</td>
		        </tr>
		      </tbody></table>
		      <p class="text-r bold">英泰伟业信息技术股份有限公司</p>
		      <p class="text-r">北京市海淀区厂洼中街66号英泰科技大厦四层</p>
		      <p class="text-r">生成日期：2016-11-20</p>
		      <h2 class="border-t">附1：积分服务账单详情</h2>
		      <table border="0" cellspacing="0" cellpadding="8" align="center" class="border">
		        <thead>
		          <tr><th>参与类型</th>
		          <th>省级积分</th>
		          <th>游戏币</th>
		          <th>金额（元）</th>
		        </tr></thead>
					<tbody><tr>
			          <th>参与兑换的数量</th>
			          <td class="text-r">5,577,000</td>
			          <td class="text-r">9,683,862,000</td>
			          <td class="text-r">--</td>
			        </tr>
			        <tr>
			          <th>参与游戏的数量</th>
			          <td class="text-r">978,142,256</td>
			          <td class="text-r">0</td>
			          <td class="text-r">--</td>
			        </tr>
			        <tr>
			          <th>本月合计</th>
			          <td class="text-r">983,719,256</td>
			          <td class="text-r">9,683,862,000</td>
			          <td class="text-r">1236333.46</td>
			        </tr>
		      </tbody>
		    </table>
		</div>
		</el-tab-pane>
	</el-tabs>
	<el-dialog :title="editFormTtile" v-model="editFormVisible">
		<div class="dtree">
<div class="dTreeNode"><img id="id0" src="../../assets/base.gif" alt="">后台管理菜单</div><div id="dd0" class="clip" style="display:block;"><div class="dTreeNode"><img id="jd1" src="../../assets/minusbottom.gif" alt=""><img id="id1" src="../../assets/folderopen.gif" alt="">系统用户管理</div><div id="dd1" class="clip" style="display: block;"><div class="dTreeNode"><img src="../../assets/empty.gif" alt=""><img id="jd2" src="../../assets/minus.gif" alt=""><img id="id2" src="../../assets/folderopen.gif" alt="">用户权限管理</div><div id="dd2" class="clip" style="display: block;"><div class="dTreeNode"><img src="../../assets/empty.gif" alt=""><img src="../../assets/line.gif" alt=""><img src="../../assets/join.gif" alt=""><img id="id3" src="../../assets/page.gif" alt="">创建用户</div><div class="dTreeNode"><img src="../../assets/empty.gif" alt=""><img src="../../assets/line.gif" alt=""><img src="../../assets/joinbottom.gif" alt=""><img id="id4" src="../../assets/page.gif" alt="">修改用户</div></div><div class="dTreeNode"><img src="../../assets/empty.gif" alt=""><img src="../../assets/join.gif" alt=""><img id="id5" src="../../assets/page.gif" alt="">用户权限查询</div><div class="dTreeNode"><img src="../../assets/empty.gif" alt=""><img src="../../assets/joinbottom.gif" alt=""><img id="id6" src="../../assets/page.gif" alt="">重置用户密码</div></div></div></div>
	</el-dialog>
</div>
</template>
<script>
	import printer from '../../utils/printer/printer.vue';
	var data = [{
		roleCode:"111",
		roleName:"业务管理员",
		roleLevel:"管理级别",
		roleDescribe:"业务管理员",
		time:"2016-08-27 17:06:59",
		lastModified:"admin",
		statu:"正常",
		remarks:"请勿修改"
	},{
		roleCode:"222",
		roleName:"业务管理",
		roleLevel:"管理级别",
		roleDescribe:"业务管理员",
		time:"2016-08-27 17:06:59",
		lastModified:"admin",
		statu:"冻结",
		remarks:"请勿修改"
	},{
		roleCode:"333",
		roleName:"总管",
		roleLevel:"管理级别",
		roleDescribe:"业务管理员",
		time:"2016-08-27 17:06:59",
		lastModified:"admin",
		statu:"销户",
		remarks:"请勿修改"
	}];
	function screen(key){
		let obj={},res = [];
		for(var i=0,len=data.length;i<len;i++){
			if(!obj[data[i][key]]){
				res.push(data[i][key]);
				obj[data[i][key]] = 1;
			}
		}
		return res;
	}
	function query(data,key,value){
		if(data instanceof Array){
			var newData = [];
			for(var i=0,len = data.length;i<len;i++){
				(data[i][key] === value) &&	newData.push(data[i]);
			}
			return newData;
		}
	}
  export default {
		data(){
			return {
				data : data,
				roleName : screen("roleName"),
				roleLevel : screen("roleLevel"),
				status : screen("statu"),
				editFormVisible:false,
				form: {
          roleName: '',
          roleLevel: '',
          statu: ''
        }
			}
		},
		components: {
			'el-print': printer
		},
    methods: {
      handleRemove(tab) {
        //console.log(tab);
      },
      handleClick(tab) {
        //console.log(tab);
      },
			open() {
        this.editFormVisible=true;
      },
			close(){
				this.editFormVisible = false;
			},
			onSubmit() {
        console.log('submit!');
      },
			handleRemove(tab) {
			 console.log(tab);
		  },
		  uploadRemove(file, fileList) {
			  console.log("remove");
        console.log(file, fileList);
      },
      uploadPreview(file) {
				console.log("preview");
        console.log(file);
      },
			uploadSuccess(a,b){
				console.log(a+" "+b);
			},
			query(){
				var roleName = this.form.roleName,
						roleLevel = this.form.roleLevel,
						statu = this.form.statu,
						newData = data;
				if(roleName) newData = query(data,"roleName",roleName);
				if(roleLevel) newData = query(newData,"roleLevel",roleLevel);
				if(statu) newData = query(newData,"statu",statu);
				this.data = newData;
			}
    }
  };
</script>
<style>
ul,li { list-style: none;}
table { border-collapse: collapse;}
.bg_table{ padding-bottom:10px; margin: 0 20px; }
.bg_table table{width:100%; table-layout:fixed;}
.bg_table tr{background:#f1f4f5;}
.bg_table th{height:30px;line-height:30px;text-align:center;background:#e0e0e0;border:1px solid #fff;font-size:14px;padding:0 2px;color:#000;}
.bg_table td{height:34px;padding:0 2px;0line-height:16px;text-align:center;border:1px solid #fff;font-size:12px;max-width:70px;word-wrap:break-word;}
.bg_table td a{color:#0e6390;font-weight:bold;text-decoration:underline;}
.bg_table td a:hover{color:#c72e3e;text-decoration:underline;}
.bg_table td strong{color:#c3c3c3}
.bg_table td .tzjlred{ color:#F00;vertical-align:middle; }
.bg_table td .tzjlblue{ color:#03F;font-style:normal;vertical-align:middle; }
.bg_table td i{ font-style:normal;vertical-align:middle; }
.dtree img {
	border: 0px;
	vertical-align: top;
}
.tj_title{width:100%;min-width:1000px;height:30px;line-height:30px;background:url(../../assets/tablebj.jpg) repeat-x;text-indent:20px;color:#fff;font-weight:bold;}
.text-r { text-align: right;}
</style>
