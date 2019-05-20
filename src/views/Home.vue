<style type="text/css">
	.container{
		padding: 10px 10px 0 10px;
		height: 98%;
		overflow: hidden;
	}

	.header{
		height: 60px;
		line-height: 60px;
		background: #1d8ce0;
		color:#fff;
	}

	.menu_and_content{
		height: 100%;
	}

	.menu_div{
		width: 250px;
		height: 100%;
		display: inline-block;
		vertical-align: top;
	}

	.content_div{
		width: calc(100% - 260px);
		height: 100%;
		display: inline-block;
	}

	.breadcrumb-container{
		margin-top:10px;
	}

	.content-wrapper{
		height: 100%;
		overflow-y: auto;
	}
</style>

<template>
	<div class="container">
		<el-row >
			<el-col  class="header">
				{{sysName}}
			</el-col>
		</el-row>

		<el-row class="menu_and_content">
			<div class="menu_div">
				<el-menu :default-active="$route.path"  @open="handleopen" @close="handleclose" @select="handleselect"
						 unique-opened router >
					<template v-for="(item,index) in $router.options.routes" v-if="!item.hidden">
						<el-submenu :index="index+''" v-if="!item.leaf">
							<template slot="title"><i :class="item.iconCls"></i>{{item.name}}</template>
							<el-menu-item v-for="child in item.children" :index="child.path" :key="child.path" v-if="!child.hidden">{{child.name}}</el-menu-item>
						</el-submenu>
						<el-menu-item v-if="item.leaf&&item.children.length>0" :index="item.children[0].path"><i :class="item.iconCls"></i>{{item.children[0].name}}</el-menu-item>
					</template>
				</el-menu>
			</div>

			<div class="content_div">
				<div class="breadcrumb-container">
					<el-breadcrumb separator="/" >
						<el-breadcrumb-item v-for="item in $route.matched" :key="item.path">
							{{ item.name }}
						</el-breadcrumb-item>
					</el-breadcrumb>
				</div>

				<div class="content-wrapper">
					<transition name="fade" mode="out-in">
						<router-view></router-view>
					</transition>
				</div>
			</div>
		</el-row>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				sysName:'奋斗的小鱼博客',
				collapsed:false,
				sysUserName: '',
				sysUserAvatar: '',
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
			handleopen() {
				//console.log('handleopen');
			},
			handleclose() {
				//console.log('handleclose');
			},
			handleselect: function (a, b) {
			},
		},
		mounted() {
			var user = sessionStorage.getItem('user');
			if (user) {
				user = JSON.parse(user);
				this.sysUserName = user.name || '';
				this.sysUserAvatar = user.avatar || '';
			}

		}
	}

</script>