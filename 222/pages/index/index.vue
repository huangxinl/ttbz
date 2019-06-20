<template>
	<view class="banner">
		<!-- 	<p style="font-family:ZoomlaXingtiJ2; "> </p> -->
		<!-- 		<view class="head">
			<text class="back iconfont"></text>
			<text class="title">{{title}}</text>
		</view> -->
		<!-- 	<view class="box">
			<text class="edit  bg-orange">单击此处编辑文字</text>
		</view> -->
		<view class="picture">
			<image src="../../static/horse.png" mode=""></image>
		</view>
		<view class="select">
			<text class="tip" style="font-family:ZoomlaXingtiJ2;">{{tip}}</text>
		</view>
		<view class="content">
			<view class="text" style="font-family:ZoomlaXingtiJ2;">
				字体大小
				<text class="boll" v-for="(item,index) in boll" @click="handSizeClick" :key="index" :data-id="item.id">{{item.size}}</text>
			</view>
			<view class="text" style="font-family:ZoomlaXingtiJ2;">
				背景颜色
				<text class="boll" v-for="(item,index) in boll" @click="handColorClick" :key="index" :data-id="item.id">{{item.bc}}</text>
			</view>
			<view class="container">
				<view class="text-color" style="font-family:ZoomlaXingtiJ2;">
					字体颜色
				</view>
				<view class="cont">
					<view class="action">
						<view data-id="1" @click="changeColor" class="cu-tag round bg-orange light" style="font-family:ZoomlaXingtiJ2;">白</view>
						<view data-id="2" @click="changeColor" class="cu-tag round bg-olive  light" style="font-family:ZoomlaXingtiJ2;">红</view>
						<view data-id="3" @click="changeColor" class="cu-tag round bg-blue light" style="font-family:ZoomlaXingtiJ2;">黑</view>
						<view data-id="4" @click="changeColor" class="cu-tag round bg-orange light" style="font-family:ZoomlaXingtiJ2;">粉</view>
						<view data-id="5" @click="changeColor" class="cu-tag round bg-olive light" style="font-family:ZoomlaXingtiJ2;">黄</view>
						<!-- 				<view class="cu-tag round bg-blue light">文</view>
						<view class="cu-tag round bg-orange light">文</view> -->
						<!-- 		<view class="cu-tag round bg-olive light">文</view>
						<view class="cu-tag round bg-blue light">文</view>
						<view class="cu-tag round bg-orange light">文</view>
						<view class="cu-tag round bg-olive light">文</view>
						<view class="cu-tag round bg-blue light">文</view> -->
					</view>
				</view>
			</view>
			<view class="padding flex flex-direction">
				<button class="cu-btn bg-red margin-tb-sm lg" style="font-family:ZoomlaXingtiJ2;">生成表情</button>
			</view>
			<input type="text" class="txt-input" v-show="flag" @touchstart="start" @touchmove="move" @input="handleKeUp"
			 @touchend="end" :style="{height,width,top:styleCss.top,left:styleCss.left,fontSize:styleCss.font,color:styleCss.color,background:styleCss.bcColor}" />
			<!-- 	<text class="txt" :style="{top:styleCss.top,left:styleCss.left,fontSize:styleCss.font,color:styleCss.color,background:styleCss.bcColor}">{{txt}}</text> -->
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				idd: 0,
				width: '100px',
				height: '30px',
				title: '表情加字',
				tip: '选择文字样式',
				boll: [{
					size: '小',
					bc: '透明',
					id: 1
				}, {
					size: '中',
					bc: '蓝',
					id: 2
				}, {
					size: '大',
					bc: '绿',
					id: 3
				}],
				flag: false,
				txt: '',
				styleCss: {
					top: 100,
					left: 150,
					font: '25px',
					color: '#000',
					bcColor: '#ffffff'
				},
				startx: 0,
				starty: 0,
				disX: 0,
				disY: 0
			}
		},
		onLoad() {

			if (this.txt) {
				return
			}
			this.flag = true
			// uni.chooseImage({
			// 	success: function(res) {
			// 		console.log(111)
			// 		var tempFilePaths = res.tempFilePaths;
			// 		uni.saveFile({
			// 			tempFilePath: tempFilePaths[0],
			// 			success: function(res) {
			// 				var savedFilePath = res.savedFilePath;
			// 			}
			// 		});
			// 	}
			// });
			
uni.downloadFile({
    url: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1561024022205&di=53f2f664c37a9de7b608cc556b27e634&imgtype=0&src=http%3A%2F%2Fe.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2F4034970a304e251fb1a2546da986c9177e3e53c9.jpg', //仅为示例，并非真实的资源
    success: function (res) {
        if (res.statusCode === 200) {
			console.log(res)
            console.log('下载成功');
        }
    }
})
		},
		methods: {
			handleKeUp(e) {
				let i = this.idd
				this.changeInput(i, e)
			},
			changeInput(i, e) {

				if (i === 1) {
					var fontone = e.detail.value.length * 17 + 'px'
					this.width = fontone
					this.height = '30px'
				} else if (i === 2) {
					var fontone = e.detail.value.length * 32 + 'px'
					this.width = fontone
					this.height = '45px'
				} else if (i === 3) {
					var fontone = e.detail.value.length * 47 + 'px'
					this.width = fontone
					this.height = '65px'
				}
			},
			changeColor(e) {
				var id = e.currentTarget.dataset.id
				if (id === "1") {
					this.styleCss.color = '#fff'
					console.log(123)
				} else if (id === "2") {
					this.styleCss.color = '#f40'
				} else if (id === "3") {
					this.styleCss.color = '#000'
				} else if (id === "4") {
					this.styleCss.color = 'pink'
				} else if (id === "5") {
					this.styleCss.color = 'yellow'
				}

			},
			start(e) {

				this.startx = e.changedTouches[0].clientX - e.currentTarget.offsetLeft
				this.starty = e.changedTouches[0].clientY - e.currentTarget.offsetTop
			},
			move(e) {
				this.disX = e.changedTouches[0].clientX - this.startx
				this.disY = e.changedTouches[0].clientY - this.starty
				// console.log(this.disX, this.disY)
				this.styleCss.top = this.disY + 'px'
				this.styleCss.left = this.disX + 'px'
			},
			end(e) {},
			// losefocurs(e) {
			// 	this.txt = e.target.value
			// },
			handSizeClick(e) {
				var id = e.currentTarget.dataset.id
				this.idd = id
				console.log(this.idd)
				if (id === 1) {
					this.styleCss.font = '15px'
					this.height = '30px'
				} else if (id === 2) {
					this.styleCss.font = '30px'
					this.height = '45px'
				} else if (id === 3) {
					this.styleCss.font = '45px'
					this.height = '65px'
				}
			},
			handColorClick(e) {
				var id = e.currentTarget.dataset.id
				if (id === 1) {
					this.styleCss.bcColor = 'transparent'
				} else if (id === 2) {
					this.styleCss.bcColor = 'blue'
				} else if (id === 3) {
					this.styleCss.bcColor = 'green'
				}
			},
			handleInput() {
				console.log(123)
			}
		}
	}
</script>

<style>
	@font-face {
		font-family: 'ZoomlaXingtiJ2';
		src: url('https://code.z01.com/font/ZoomlaXingtiJ2.eot?#iefix');
		/* IE9 */
		src: url('https://code.z01.com/font/ZoomlaXingtiJ2.eot?#iefix') format("embedded-opentype"),
			/* IE6-IE8 */
			url('https://code.z01.com/font/ZoomlaXingtiJ2.woff') format("woff"),
			/* chrome、firefox */
			url('https://code.z01.com/font/ZoomlaXingtiJ2.ttf') format("truetype"),
			/* chrome、firefox、opera、Safari, Android, iOS 4.2+ */
			url('https://code.z01.com/font/ZoomlaXingtiJ2.svg#ZoomlaXingtiJ2') format("svg");
		/* iOS 4.1- */
		font-style: normal;
		font-weight: normal;
	}

	.banner {
		position: relative;
	}

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
		position: absolute;
		top: 205px;
		left: 145px;
		border-radius: 15upx;
		background: #fff;
		text-align: center;
	}

	/* 	.txt {
		position: absolute;
		border-radius: 15upx;
		background: #fff;
	} */

	.picture {
		text-align: center;
	}

	/* 	image {
		margin: 0 auto;
	} */
</style>
