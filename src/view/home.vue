<template>
	<div class="pos">
		<div>
			<el-row>
                <el-col :span='7' id="list">
                    <el-tabs> 
                        <el-tab-pane label='点餐'>
                            <el-table :data='tableData' border show-summary style="width:100%">
                                <el-table-column label='商品' prop='name'></el-table-column>
                                <el-table-column label='数量' prop='count'></el-table-column>
                                <el-table-column label='金额' prop='pri'></el-table-column>
                                <el-table-column label='操作' width='150'>
                                	<template slot-scope="scope">
                                			<el-button type="primary" plain size='mini'>删除</el-button>
                                        	<el-button type="primary" plain size='mini'>新增</el-button>
                                	</template>
                                </el-table-column>
                            </el-table>
                        </el-tab-pane>
                        <el-row style="text-align: center;margin-top:20px ">
			            	<el-button type="danger">清空</el-button>
			  				<el-button type="success">结账</el-button>
			            </el-row>
                        <el-tab-pane label='外卖'>
                            外卖
                        </el-tab-pane>
                    </el-tabs>
                </el-col>
                <el-col :span='14'>
                    <div class="pro">
                    	<div class="title">热门商品</div>
                    	<div class="pro-list">
                    		<ul>
                    			<li v-for='val in pros'>
                    				<span>{{val.name}}</span>
                    				<span class="pro-pri">￥{{val.pri}}</span>
                    			</li>
                    		</ul>
                    	</div>
                    </div>
                    <div class="pro-type">
                        <el-tabs>
                            <el-tab-pane label='肥宅区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType1'>
                                        <span class="foodImg"><img :src="val.img" alt=""></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label='儿童区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType2'>
                                        <span class="foodImg"><img :src="val.img" alt=""></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label='LLY区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType3'>
                                        <span class="foodImg"><img :src="val.img" alt=""></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                        </el-tabs>
                    </div>
                </el-col>
            </el-row>	
		</div>
	</div>
</template>

<script>
	import axios from 'axios'
	export default{
		data(){
			return{
				tableData:'',
				pros:'',
				goodType1:'',
				goodType2:'',
				goodType3:''
			}
		},
		mounted(){
			let h=document.body.clientHeight;
			let list=document.querySelector('#list');
			list.style.height=h+'px';
		},
		created(){
			axios.get('http://localhost:8080/static/data.json')
			.then(res=>{
				this.tableData=res.data.tableData;
				this.pros=res.data.pros;
				this.goodType1=res.data.goodType1;
				this.goodType2=res.data.goodType2;
				this.goodType3=res.data.goodType3;
			})
			.catch(err=>{
				console.log('网络不给力');
			})
		}
	}
</script>
<style scoped>
	.pro{
		width: 100%;
	}
	.title{
		width: 100%;
		text-align: center;
		height: 50px;
		line-height: 50px;
		background: #252525;
		color: #d92353;
		font-size: 18px;
		font-weight: 700;
	}
	.pro-list li{
		list-style: none;
		padding: 10px;
		margin-left: 20px; 
		float: left;
		border:1px solid #d92353;
		cursor: pointer;
	}
	.pro-pri{
		color: #ce0000;
		font-weight: 700;
	}
	.pro-type{
		display: block;
		clear: both;
	}
	.ckList{
		list-style: none;
	}
	.ckList>li{
		float: left;
		width: 20%;
		height: 200px;
		margin-left: 20px;
		position: relative;
	}
	.ckList img{
		width: 100%;
		height: 100%;
		display: block;
	}
	.foodName{
		position: absolute;
		z-index: 10;
		top: 0;
		left: 50%;
		transform: translateX(-50%);
		font-size: 16px;
		font-weight: 700;
	}
	.foodPri{
		position: absolute;
		z-index: 10;
		top: 0;
		color:#333;
		font-size: 18px;
		font-weight: 900;
	}
</style>