<template>
	<div>
	<el-tabs style="width:100%;" type="card" @tab-click="handleClick" @tab-remove="handleRemove">
		<el-tab-pane label="用户管理">
			<el-col :span="24" style="padding:10px;">
				<el-steps :space="100" direction="vertical" :active="1">
					<el-step title="步骤 1"></el-step>
					<el-step title="步骤 2"></el-step>
					<el-step title="步骤 3"></el-step>
				</el-steps>
			</el-col>
		</el-tab-pane>
		<el-tab-pane label="配置管理">222</el-tab-pane>
		<el-tab-pane label="角色管理">
		<div class="bgtj">
			<ul class="tj_title">
				<li>查询条件</li>
			</ul>
			<ul class="bg_tjtab">
				<li class="bg_tjall">
					<table>
						<tbody>
							<tr>
								<th>角色名称</th>
								<td>
									<select name="roleName" id="roleName">
										<option value="">全部</option>
										<option v-for="value in roleName">{{value}}</option>
									</select>
								</td>
								<th>角色级别</th>
								<td>
									<select name="roleLevel" id="roleLevel">
										<option value="">全部</option>
										<option v-for="value in roleLevel">{{value}}</option>
									</select>
								</td>
							</tr>
							<tr>
								<th>状态</th>
								<td>
									<select name="state" id="state">
										<option value="">全部</option>
										<option value="0">正常</option>
										<option value="1">冻结</option>
										<option value="2">注销</option>
									</select>
								</td>
								<th></th>
								<td></td>
							</tr>
						</tbody>
					</table>
				</li>
				<li class="bg_button"><a href="javascript:void(0);" onclick="invokeAction('list');">查询</a></li>
			</ul>
		</div>
			<div class="bg_table">
				<table cellspacing="0" cellpadding="0" border="0" class="bg_odd">
					<tr>
						<th>序号</th>
						<th>角色代码</th>
						<th>角色名称</th>
						<th>角色级别</th>
						<th>角色描述</th>
						<th>最后修改时间</th>
						<th>最后修改人</th>
						<th>状态</th>
						<th>备注</th>
						<th>操作</th>
					</tr>
					<tr v-for="(value,key) in data">
						<td>{{key+1}}</td>
						<td>{{value.roleCode}}</td>
						<td>{{value.roleName}}</td>
						<td>{{value.roleLevel}}</td>
						<td>{{value.roleDescribe}}</td>
						<td>{{value.time}}</td>
						<td>{{value.lastModified}}</td>
						<td>{{status[value.statu]}}</td>
						<td>{{value.remarks}}</td>
						<td><a href="javascript:;"  @click="open">查看角色功能</a></td>
					</tr>
				</table>
			</div>
		</el-tab-pane>
		<el-tab-pane label="定时任务补偿">444</el-tab-pane>
	</el-tabs>
	<el-dialog :title="editFormTtile" v-model="editFormVisible">
		<div class="dtree">
<div class="dTreeNode"><img id="id0" src="/tools/dtree/img/base.gif" alt="">后台管理菜单</div><div id="dd0" class="clip" style="display:block;"><div class="dTreeNode"><a href="javascript: d.o(1);"><img id="jd1" src="/tools/dtree/img/minusbottom.gif" alt=""></a><img id="id1" src="/tools/dtree/img/folderopen.gif" alt=""><a href="javascript: d.o(1);" class="node">系统用户管理</a></div><div id="dd1" class="clip" style="display: block;"><div class="dTreeNode"><img src="/tools/dtree/img/empty.gif" alt=""><a href="javascript: d.o(2);"><img id="jd2" src="/tools/dtree/img/minus.gif" alt=""></a><img id="id2" src="/tools/dtree/img/folderopen.gif" alt=""><a href="javascript: d.o(2);" class="node">用户权限管理</a></div><div id="dd2" class="clip" style="display: block;"><div class="dTreeNode"><img src="/tools/dtree/img/empty.gif" alt=""><img src="/tools/dtree/img/line.gif" alt=""><img src="/tools/dtree/img/join.gif" alt=""><img id="id3" src="/tools/dtree/img/page.gif" alt="">创建用户</div><div class="dTreeNode"><img src="/tools/dtree/img/empty.gif" alt=""><img src="/tools/dtree/img/line.gif" alt=""><img src="/tools/dtree/img/joinbottom.gif" alt=""><img id="id4" src="/tools/dtree/img/page.gif" alt="">修改用户</div></div><div class="dTreeNode"><img src="/tools/dtree/img/empty.gif" alt=""><img src="/tools/dtree/img/join.gif" alt=""><img id="id5" src="/tools/dtree/img/page.gif" alt="">用户权限查询</div><div class="dTreeNode"><img src="/tools/dtree/img/empty.gif" alt=""><img src="/tools/dtree/img/joinbottom.gif" alt=""><img id="id6" src="/tools/dtree/img/page.gif" alt="">重置用户密码</div></div></div></div>
	</el-dialog>
</div>
</template>
<script>
	var data = [{
		roleCode:"111",
		roleName:"业务管理员",
		roleLevel:"管理级别",
		roleDescribe:"业务管理员",
		time:"2016-08-27 17:06:59",
		lastModified:"admin",
		statu:"0",
		remarks:"预制角色，请勿修改"
	},{
		roleCode:"222",
		roleName:"业务管理",
		roleLevel:"管理级别",
		roleDescribe:"业务管理员",
		time:"2016-08-27 17:06:59",
		lastModified:"admin",
		statu:"1",
		remarks:"预制角色，请勿修改"
	},{
		roleCode:"333",
		roleName:"总管",
		roleLevel:"管理级别",
		roleDescribe:"业务管理员",
		time:"2016-08-27 17:06:59",
		lastModified:"admin",
		statu:"0",
		remarks:"预制角色，请勿修改"
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
  export default {
		data(){
			return {
				data:data,
				roleName : screen("roleName"),
				roleLevel : screen("roleLevel"),
				statu : screen("statu"),
				status : ["正常","冻结","注销"],
				editFormVisible:false
			}
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
.bg_table td{height:34px;padding:0 2px;line-height:16px;text-align:center;border:1px solid #fff;font-size:12px;max-width:70px;word-wrap:break-word;}
.bg_table td a{color:#0e6390;font-weight:bold;text-decoration:underline;}
.bg_table td a:hover{color:#c72e3e;text-decoration:underline;}
.bg_table td strong{color:#c3c3c3}
.bg_table td .tzjlred{color:#F00;vertical-align:middle;}
.bg_table td .tzjlblue{color:#03F;font-style:normal;vertical-align:middle;}
.bg_table td i{font-style:normal;vertical-align:middle;}
.tj_bt{color:#F00;font-size:14px;}
.bg_button{width:100%;min-width:1000px;height:60px;line-height:50px;padding-top:10px;text-align:center;}
.bg_button a,.btn,.btn-2{vertical-align:middle;display:inline-block;width:100px;height:30px;line-height:30px;text-align:center;color:#fff;background:url(../../assets/tablebj.jpg) repeat-x;margin-right:20px;cursor:pointer;border:none;}
.bg_button a:hover,.btn:hover,.btn-2:hover{color:#fff;background:#c72c3e;}
.bg_tjtab { margin: 0 20px; padding: 0;}
.bg_tjall table{width:100%;min-width:1000px;}
.bg_tjall th{width:130px;height:36px;line-height:16px;text-align:right;background:#ecf0f1;border:1px solid #fff;font-size:12px;padding:0 8px 0 0;font-weight:normal;}
.bg_tjall td{height:36px;padding-left:6px;line-height:16px;text-align:left;border:1px solid #fff;font-size:12px;background:#ecf0f1;}
.bg_tjall input{width:200px;height:22px;line-height:22px;font-size:12px;border:1px solid #c7c7c7;background:#fff;}
.bg_tjall select{width:202px;height:24px;line-height:24px;font-size:12px;border:1px solid #c7c7c7;background:#fff;}
.bg_tjall textarea{width:200px;font-size:12px;border:1px solid #c7c7c7;}
.bg_tjall .dxbtn{width:14px;height:14px;border:none;}
.bg_tjall .timetj{font-weight:normal;margin-right:20px;}
.bg_tjall .five{width:8%;}
.bg_tjall .errred{color:#c72c3e;}

.tj_title{width:100%;min-width:1000px;height:30px;line-height:30px;background:url(../../assets/tablebj.jpg) repeat-x;text-indent:20px;color:#fff;font-weight:bold;}
</style>
