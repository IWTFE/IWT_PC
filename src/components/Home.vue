<template>
	<el-row class="panel">
		<el-col :span="24" class="panel-top">
			<el-col :span="20" class="logo"></el-col>
			<el-col :span="4" class="right-opt">
				<el-breadcrumb separator="|">
				  <el-breadcrumb-item :to="{ path: '/' }">
				  	<img src="../assets/user.png" style="vertical-align: middle;" alt="" />
				  </el-breadcrumb-item>
				  <el-breadcrumb-item>系统管理员</el-breadcrumb-item>
				  <el-breadcrumb-item  :to="{ path: '/' }">安全退出</el-breadcrumb-item>
				</el-breadcrumb>
			</el-col>
		</el-col>
		<el-col :span="24" class="panel-center">
			<!--<el-col :span="4">-->
			<aside style="width:230px;">
				<el-menu default-active="/table" class="el-menu-vertical-demo" @open="handleopen"
					@close="handleclose" @select="handleselect" theme="light" unique-opened router>
					<el-submenu index="1">
						<template slot="title"><i class="el-icon-message"></i>广告管理</template>
						<el-menu-item index="/table">列表</el-menu-item>
						<el-menu-item index="/form">发布广告</el-menu-item>
						<el-menu-item index="/page3">用户管理</el-menu-item>
					</el-submenu>
					<el-submenu index="2">
						<template slot="title"><i class="fa fa-id-card-o"></i>导航二</template>
						<el-menu-item index="/page4">选项4</el-menu-item>
						<el-menu-item index="/page5">选项5</el-menu-item>
					</el-submenu>
					<el-menu-item index="/page6"><i class="fa fa-line-chart"></i>导航三</el-menu-item>

				</el-menu>
			</aside>
			<!--</el-col>-->
			<!--<el-col :span="20" class="panel-c-c">-->
			<section class="panel-c-c">
				<div class="grid-content bg-purple-light">
					<el-col :span="24" style="margin-bottom:15px;border-bottom: 1px solid #d9d9d9;">
						<p class="current-path">您现在的位置：{{currentPathNameParent}} > {{currentPathName}}</p>
					</el-col>
					<el-col :span="24" style="background-color:#fff;box-sizing: border-box;">
						<transition name="fade">
							<router-view></router-view>
						</transition>
					</el-col>
				</div>
			</section>
			<!--</el-col>-->
		</el-col>
	</el-row>
</template>

<script>
  export default {
    data() {
      return {
		  currentPathName:'Table',
		  currentPathNameParent:'导航一',
        form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        }
      }
    },
	watch: {
		'$route' (to, from) {//监听路由改变
			this.currentPathName=to.name;
			this.currentPathNameParent=to.matched[0].name;
		}
	},
    methods: {
      onSubmit() {
        console.log('submit!');
      },
			handleopen(){
				//console.log('handleopen');
			},
			handleclose(){
				//console.log('handleclose');
			},
            handleselect:function(a,b){
            },
			//退出登录
			logout:function(){
				var _this=this;
				this.$confirm('确认退出吗?', '提示', {
					//type: 'warning'
				}).then(() => {
					_this.$router.replace('/login');
				}).catch(() => {

				});


			}
    }
  }
</script>

<style>

	.fade-enter-active,
	.fade-leave-active {
		transition: opacity .5s
	}

	.fade-enter,
	.fade-leave-active {
		opacity: 0
	}

	.panel {
		position: absolute;
		top: 0px;
		bottom: 0px;
		width: 100%;
	}

	.panel-top {
		height: 78px;
		line-height: 78px;
		background: url(../assets/top-bj.jpg) repeat-x;
		color: #c0ccda;
	}

	.panel-center {
		background: #ecf0f1;
		position: absolute;
		top: 78px;
		bottom: 0px;
		overflow: hidden;
	}

	.panel-c-c {
		background: #f1f2f7;
		position: absolute;
		right: 0px;
		top: 0px;
		bottom: 0px;
		left: 230px;
		overflow-y: scroll;
		padding: 10px;
	}

	.logout {
		background: url(../assets/logout_36.png);
		background-size: contain;
		width: 20px;
		height: 20px;
		float: left;
	}

	.logo {
		height: 78px;
		background:url(../assets/top-logo.jpg) no-repeat;
	}

	.tip-logout {
		float: right;
		margin-right: 20px;
		padding-top: 5px;
		cursor: pointer;
	}

	.admin {
		color: #c0ccda;
		text-align: center;
	}
	.right-opt .el-breadcrumb{
		font-size: 14px;
		line-height: 78px;
	}

	.current-path{
		margin: 8px auto;
		text-indent: 28px;
		background: url(../assets/bg-wzico.png) no-repeat 10px 8px;
		background-position: 0 center;
		float:left;
		font-size: 12px;
		color: #a6a6a6;
	}
	.el-menu--horizontal.el-menu--dark .el-submenu .el-menu-item.is-active, .el-menu-item.is-active {
	    background: #bc1b2e;
			color: #fff;
	}
	.el-menu--horizontal.el-menu--dark .el-submenu .el-menu-item:hover, .el-menu-item:hover {
	    background: #bc1b2e;
			color: #fff;
	}
	.el-submenu .el-menu {
    background-color: #e5e9f2;
	}
	.el-menu {
    background-color: #e5e9f2;
	}
	.right-opt .el-breadcrumb__item__inner, .right-opt .el-breadcrumb__item .el-breadcrumb__item__inner{
	  color: #fff;
	  cursor: pointer;
	}
	.el-submenu .el-menu-item:hover, .el-submenu__title:hover {
			background: #bc1b2e;
			color: #fff;
	}
</style>
