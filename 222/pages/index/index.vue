<template>
	<view class="banner">
		<!-- 		<view class="head">
			<text class="back iconfont"></text>
			<text class="title">{{title}}</text>
		</view> -->
		<view class="box">
			<text class="edit  bg-orange">单击此处编辑文字</text>
		</view>
		<view class="select">
			<text class="tip">{{tip}}</text>
		</view>
		<view class="content">
			<view class="text">
				字体大小
				<text class="boll" v-for="(item,index) in boll" :key="index">{{item.size}}</text>
			</view>
			<view class="text">
				背景颜色
				<text class="boll" v-for="(item,index) in boll" :key="index">{{item.bc}}</text>
			</view>
			<view class="container">
				<view class="text-color">
					字体颜色
				</view>
				<view class="cont">
					<view class="action">
						<view @click="changeColor" class="cu-tag round bg-orange light">文</view>
						<view class="cu-tag round bg-olive  light">文</view>
						<view class="cu-tag round bg-blue light">文</view>
						<view class="cu-tag round bg-orange light">文</view>
						<view class="cu-tag round bg-olive light">文</view>
						<view class="cu-tag round bg-blue light">文</view>
						<view class="cu-tag round bg-orange light">文</view>
						<view class="cu-tag round bg-olive light">文</view>
						<view class="cu-tag round bg-blue light">文</view>
						<view class="cu-tag round bg-orange light">文</view>
						<view class="cu-tag round bg-olive light">文</view>
						<view class="cu-tag round bg-blue light">文</view>
					</view>
				</view>
			</view>
			<view class="padding flex flex-direction">
				<button class="cu-btn bg-grey lg" @click="addtxt">新增文本框</button>
				<button class="cu-btn bg-red margin-tb-sm lg">生成表情</button>
			</view>
			<input type="text" class="txt-input" value="" placeholder="请输入文本" v-show="flag" @touchstart="start" @touchmove="move"
			 @touchend="end" @blur="losefocurs" :style="{top:styleCss.top,left:styleCss.left,fontSize:styleCss.font,color:styleCss.color}" />
			<text class="txt" :style="{top:styleCss.top,left:styleCss.left,fontSize:styleCss.font,color:styleCss.color}">{{txt}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '表情加字',
				tip: '选择文字样式',
				boll: [{
					size: '小',
					bc: '透明',
					id: 1
				}, {
					size: '中',
					bc: '白',
					id: 2
				}, {
					size: '大',
					bc: '黑',
					id: 3
				}],
				flag: false,
				txt: '',
				styleCss: {
					top: 0,
					left: 0,
					font: '25px',
					color: '#f40'
				},
				startx: 0,
				starty: 0,
				disX: 0,
				disY: 0
			}
		},
		onLoad() {

		},
		methods: {
			changeColor() {
				console.log(123)
			},
			start(e) {
				this.startx = e.changedTouches[0].clientX - e.currentTarget.offsetLeft
				this.starty = e.changedTouches[0].clientY - e.currentTarget.offsetTop

			},
			move(e) {
				console.log('move')
				console.log(e)
				this.disX = e.changedTouches[0].clientX - this.startx
				this.disY = e.changedTouches[0].clientY - this.starty
				console.log(this.disX, this.disY)
				this.styleCss.top = this.disY + 'px'
				this.styleCss.left = this.disX + 'px'
			},
			end(e) {
				console.log('end')
				// console.log(this.styleCss)
			},
			addtxt() {
				// if(this.txt) {
				// 	return
				// }


				// this.styleCss.top = Math.random()*100
				// this.styleCss.left = Math.random()*100
				this.flag = true
			},
			losefocurs(e) {
				this.txt = e.target.value
				this.flag = false
			
			},
		}
	}
</script>

<style>
	.back::before {
		content: '<';

	}

	.head,
	.select {
		height: 60upx;
		line-height: 60upx;
		text-align: center;
		padding: 0 20upx;
		background: #888;
	}

	/* 	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	} */

	/* .title {
		font-size: 28upx;
		color: #000;
		font-weight: bold;
	}

	.back {
		position: absolute;
		left: 10upx;
	} */

	.box {
		position: relative;
		margin: 50rpx auto;
		border: 1px solid #888888;
		width: 300rpx;
		height: 200rpx;
		padding: 10rpx;
		text-align: center;

	}

	.edit {
		font-size: 24upx;
	}

	.tip {
		font-size: 28upx;
		color: #000;
		font-weight: bold;
		float: left;
	}

	.text {
		font-size: 20upx;
		padding: 20upx;
	}

	.boll {
		display: inline-block;
		text-align: center;
		line-height: 50upx;
		width: 50upx;
		height: 50upx;
		margin-bottom: 10upx;
		margin-left: 40upx;
		border: 1px solid #888888;
		/* background: #888888; */
		color: #000000;
		border-radius: 50%;
		font-size: 20upx;
	}

	.text-color {
		flex: 0 0 150upx;
		font-size: 20upx;
		padding: 20upx;
	}

	.container {
		display: flex;
	}

	.cont {
		flex: 1;
	}

	.cu-tag:nth-child(1) {
		margin-left: 10upx;
	}

	.cu-tag {
		border-radius: 50%;
		margin: 0 20upx 20upx;
	}

	.txt-input {
		width: 50%;
		position: absolute;
		top: 40upx;
		left: 80upx;
		padding: 10upx;
		border-radius: 15upx;
		border: 1px solid #007AFF;
		color: #ffff;
	}
	
	.txt {
		position: absolute;
		padding: 10upx;
		color: #ffff
	}
	
</style>
