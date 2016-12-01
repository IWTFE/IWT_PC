<template>
	<section>导出excel
		<export-excel :listData="tableData"></export-excel>
	</section>
</template>
<script type="text/javascript">
	import excelVue from '../../utils/exportExcel/exportExcel.vue';
	export default{
		data: function(){
			return {
				tableData: [
				{"title": ["#", "姓名", "年龄", "生日", "地址" ]}
				,{
					id:1000,
					name: 'lanqy1',
					age: 20,
					birth:'1996-03-02',
					addr:'广东广州天河体育中心'
				}, {
					id:1001,
					name: 'lanqy2',
					age: 20,
					birth:'1996-03-02',
					addr:'广东广州天河体育中心'
				}, {
					id:1002,
					name: 'lanqy3',
					age: 20,
					birth:'1996-03-02',
					addr:'广东广州天河体育中心'
				}, {
					id:1003,
					name: 'lanqy4',
					age: 20,
					birth:'1996-03-02',
					addr:'广东广州天河体育中心'
				}, {
					id:1004,
					name: 'lanqy5',
					age: 20,
					birth:'1996-03-02',
					addr:'广东广州天河体育中心'
				}, {
					id:1005,
					name: 'lanqy6',
					age: 20,
					birth:'1996-03-02',
					addr:'广东广州天河体育中心'
				}, {
					id:1006,
					name: 'lanqy7',
					age: 20,
					birth:'1996-03-02',
					addr:'广东广州天河体育中心'
				}, {
					id:1007,
					name: 'lanqy8',
					age: 20,
					birth:'1996-03-02',
					addr:'广东广州天河体育中心'
				}]
			}
		},
		components: {
			'export-excel': excelVue
		}
	}
</script>
