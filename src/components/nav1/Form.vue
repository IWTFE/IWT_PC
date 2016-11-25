<template>
	<el-form ref="form" :model="form" label-position="center" label-width="100px" @submit.prevent="onSubmit" style="margin:10px;width:60%;min-width:600px;">
		<el-tabs type="card" @tab-click="handleClick" @tab-remove="handleRemove">
	    <el-tab-pane label="发布广告:">
				<el-form-item label="标题：">
					<el-input v-model="form.name"></el-input>
				</el-form-item>
				<el-form-item label="有效期:">
					<el-col :span="11">
						<el-date-picker type="date" placeholder="开始日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
					</el-col>
					<el-col class="line" :span="2" style="text-align:center">至</el-col>
					<el-col :span="11">
						<el-date-picker type="date" placeholder="结束日期" v-model="form.date2" style="width: 100%;"></el-date-picker>
					</el-col>
				</el-form-item>
				<el-form-item label="顺序号:">
					<el-input v-model="form.name"></el-input>
				</el-form-item>
				<el-form-item label="投放位置:">
					<el-select v-model="form.region" placeholder="请选择活动区域">
						<el-option label="区域一" value="shanghai"></el-option>
						<el-option label="区域二" value="beijing"></el-option>
					</el-select>
				</el-form-item>
				<el-form-item label="上传图像:">
					<el-upload
					  action="//jsonplaceholder.typicode.com/posts/"
					  type="drag"
					  :multiple="true"
					  :on-preview="uploadPreview"
					  :on-remove="uploadRemove"
					  :on-success="uploadSuccess"
					  :on-error="uploadError"
					>
					  <i class="el-icon-upload"></i>
					  <div class="el-dragger__text">将文件拖到此处，或<em>点击上传</em></div>
					  <div class="el-upload__tip" slot="tip">只能上传jpg/png文件，且不超过500kb</div>
					</el-upload>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" @click="onSubmit">发布</el-button>
					<el-button>重置</el-button>
				</el-form-item>
			</el-tab-pane>
		  <el-tab-pane label="所有广告">所有广告</el-tab-pane>
	  </el-tabs>
	</el-form>
</template>

<script>
  export default {
    data() {
      return {
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
    methods: {
      onSubmit() {
        console.log('submit!');
      },
			handleRemove(tab) {
			 console.log(tab);
		 },
		 handleClick(tab, event) {
			 console.log(tab, event);
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
			}
    }
  }
</script>
<style scoped>
	.el-tabs{
		width: 100%;
	}
	.el-form-item{
		text-align: left
	}
</style>
