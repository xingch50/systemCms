<template>
	<div>
		<el-table size="mini" :fit="false" ref="multipleTable" :data="dataArray"  border style="width: 100%" :header-cell-style="{background:'#f5f7fa'}">
			<!-- 判断是否显示复选框  isSelection true flase -->
			<div v-if="isSelection == true">
				<el-table-column type="selection" width="50"></el-table-column>
			</div>

      <!--

       show-overflow-tooltip
        tooltip-effect="dark"

      -->

			<el-table-column v-for="(column, index) in columns" :label="column.label" :prop="column.prop" :key="index" :width="column.width">
				<template slot-scope="scope">
					<my-render v-if="column.render" :row="scope.row" :render="column.render"></my-render>
					<span v-else>
                    	{{scope.row[column.prop]}}
                    </span>
				</template>
			</el-table-column>
		</el-table>

		<div class="block" style="margin-top: 15px; overflow: hidden;">
			<el-pagination :size-change="pageSize" :current-change="pageNum" @current-change="getArticle" :page-size="10" layout="total, prev, pager, next, jumper" :total="total">
			</el-pagination>
		</div>
	</div>
</template>

<script>
import MyRender from '@/components/common/MyRender'
export default {
    props: ['dataArray', 'columns', 'isSelection', 'pageSize', 'pageNum', 'total' ],
    methods: {
        getArticle(val) {
            this.$emit('getArticle', val)
        }
    },
    components: {
        MyRender
    }
}
</script>

<style>
table {
	width: 100% !important;
}
</style>

