<template>
	<view class="banner">
		<avatar selWidth="200px" selHeight="400upx" @upload="myUpload" :avatarSrc="url" avatarStyle="width: 100%; height: 250px; border-radius:0 ">
		</avatar>
		<!-- 		<view class="picture">
			<image src="../../static/horse.png" mode=""></image>
		</view> -->
		<view class="select">
			<text class="tip">{{tip}}</text>
		</view>
		<view class="content">
			<view class="text">
				字体大小
				<text :class="['boll',{'active': index+1 === idd}]" v-for="(item,index) in boll" @click="handSizeClick" :key="index"
				 :data-id="item.id">{{item.size}}</text>
			</view>
			<view class="text">
				背景颜色
				<text :class="['boll',{'light': index+1 === colorId}]" v-for="(item,index) in boll" @click="handColorClick" :key="index"
				 :data-id="item.id">{{item.bc}}</text>
			</view>
			<view class="container">
				<view class="text-color">
					字体颜色
				</view>
				<view class="cont">
					<view class="action">
						<view data-id="1" @click="changeColor" class="cu-tag round bg-orange light">红</view>
						<view data-id="2" @click="changeColor" class="cu-tag round bg-olive  light">橙</view>
						<view data-id="3" @click="changeColor" class="cu-tag round bg-blue light">黄</view>
						<view data-id="4" @click="changeColor" class="cu-tag round bg-orange light">绿</view>
						<view data-id="5" @click="changeColor" class="cu-tag round bg-olive light">青</view>
						<view data-id="6" @click="changeColor" class="cu-tag round bg-blue light">蓝</view>
						<view data-id="7" @click="changeColor" class="cu-tag round bg-orange light">紫</view>
						<view data-id="8" @click="changeColor" class="cu-tag round bg-olive light">白</view>
						<view data-id="9" @click="changeColor" class="cu-tag round bg-blue light">灰</view>
						<view data-id="10" @click="changeColor" class="cu-tag round bg-orange light">文</view>
						<view data-id="11" @click="changeColor" class="cu-tag round bg-olive light">文</view>
						<view data-id="12" @click="changeColor" class="cu-tag round bg-blue light">文</view>
					</view>
				</view>
			</view>
			<view class="padding flex flex-direction">
				<button class="cu-btn bg-red margin-tb-sm lg" @click="handleNewFace">生成表情</button>
				<button class="cu-btn bg-red margin-tb-sm lg"  @click="addText">新增文本框</button>
			</view>
			<view class="trag" :style="{top:styleCss.top,left:styleCss.left,height,width,background:styleCss.bcColor}" @touchstart="start" @touchmove="move"  v-show="flag"
			 @touchend="end">
				<input type="text" class="txt-input" @blur="losefocurs" @input="handleKeUp" placeholder="编辑文字" :style="{height,width,fontSize:styleCss.font,color:styleCss.color,background:styleCss.bcColor}" />
				<text class="lg text-gray cuIcon-roundclosefill close" @click="handleCloseClick" v-show="index"></text>
			</view>
			{{str}}
			<view v-html=""></view>
			<!-- <h1 style="font-family:ZoomlaXingtiJ; font-weight:500; font-size:4em;"> 中国字体网，做中国最优秀的字体研发中心！</h1> -->
			<text class="txt" :style="{top:styleCss.top,left:styleCss.left,fontSize:styleCss.font,color:styleCss.color,background:styleCss.bcColor}">{{txt}}</text>
		</view>
	</view>
</template>

<script>
	import avatar from "../../components/yq-avatar/yq-avatar.vue";
	export default {
		components: {
			avatar
		},
		data() {
			return {
				str: `<text>45454</text>`,
				index:1,
				len: 0,
				textInput: '',
				colorId: 0,
				url: "../../static/horse.png",
				idd: 1,
				width: '120px',
				height: '30px',
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
					top: 100,
					left: 150,
					font: '15px',
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

			// uni.downloadFile({
			//     url: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1561024022205&di=53f2f664c37a9de7b608cc556b27e634&imgtype=0&src=http%3A%2F%2Fe.hiphotos.baidu.com%2Fimage%2Fpic%2Fitem%2F4034970a304e251fb1a2546da986c9177e3e53c9.jpg', //仅为示例，并非真实的资源
			//     success: function (res) {
			//         if (res.statusCode === 200) {
			// 			console.log(res)
			//             console.log('下载成功');
			//         }
			//     }
			// })
		},
		methods: {
			myUpload(rsp) {
				this.url = rsp.path; //更新头像方式一
				//rsp.avatar.imgSrc = rsp.path; //更新头像方式二
			},
			handleKeUp(e) {
				if (e.detail.value.length === 0) {
					e.detail.value = '     '
				}
				this.textInput = e.target.value
				let i = this.idd
				this.len = e.detail.value.length
				this.changeInput(i, this.len)
			},
			changeInput(i, len) {
				this.changeWidth(i, len)
			},
			changeWidth(i, len) {
				if (i === 1) {
					var fontone = len * 17 + 'px'
					this.width = fontone
					this.height = '30px'
				} else if (i === 2) {
					var fontone = len * 32 + 'px'
					this.width = fontone
					this.height = '45px'
				} else if (i === 3) {
					var fontone = len * 47 + 'px'
					this.width = fontone
					this.height = '65px'
				}
			},
			changeColor(e) {
				var id = e.currentTarget.dataset.id
				id = JSON.parse(id)
				switch (id) {
					case 1:
						this.styleCss.color = '#f40'
						break;
					case 2:
						this.styleCss.color = '#F40'
						break;
					case 3:
						this.styleCss.color = 'red'
						break;
					case 4:
						this.styleCss.color = '#0C0'
						break;
					case 5:
						this.styleCss.color = '#699'
						break;
					case 6:
						this.styleCss.color = '#06C'
						break;
					case 7:
						this.styleCss.color = '#909'
						break;
					case 8:
						this.styleCss.color = '#fff'
						break;
					case 9:
						this.styleCss.color = '#455'
						break;
					case 10:
						this.styleCss.color = '#ccc'
						break;
					case 11:
						this.styleCss.color = '#555'
						break;
					case 12:
						this.styleCss.color = '#777'
						break;
					default:
						this.styleCss.color = '#999'
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
			losefocurs(e) {
				console.log(e)
				// this.txt = e.target.value
				this.handleKeUp(e)
			},
			handSizeClick(e) {
				this.key = true
				var id = e.currentTarget.dataset.id
				this.idd = id
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
				this.changeInput(this.idd, this.len)
			},
			handColorClick(e) {
				var id = e.currentTarget.dataset.id
				this.colorId = id
				if (id === 1) {
					this.styleCss.bcColor = 'transparent'
				} else if (id === 2) {
					this.styleCss.bcColor = '#fff'
				} else if (id === 3) {
					this.styleCss.bcColor = '#000'
				}
			},
			handleCloseClick() {
				this.flag = !this.flag
			},
			handleNewFace() {
				this.index = 0
			},
			addText() {
				
			}
		}
	}
</script>

<style>
	@font-face {
		font-family: 'ZoomlaXingtiJ';
		src: url('https://code.z01.com/font/ZoomlaXingtiJ.eot?#iefix');
		/* IE9 */
		src: url('https://code.z01.com/font/ZoomlaXingtiJ.eot?#iefix') format("embedded-opentype"),
			/* IE6-IE8 */
			url('https://code.z01.com/font/ZoomlaXingtiJ.woff') format("woff"),
			/* chrome、firefox */
			url('https://code.z01.com/font/ZoomlaXingtiJ.ttf') format("truetype"),
			/* chrome、firefox、opera、Safari, Android, iOS 4.2+ */
			url('https://code.z01.com/font/ZoomlaXingtiJ.svg#ZoomlaXingtiJ') format("svg");
		/* iOS 4.1- */
		font-style: normal;
		font-weight: normal;
	}

	.banner {
		width: 100%;
		overflow: hidden;
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
		max-width: 300px;
		font-family: ZoomlaXingtiJ;
		border-radius: 15upx;
		background: #fff;
		text-align: center;
	/* 	border: 1px solid #fff; */
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
	.active {
		background: #0081FF;
	}

	.light {
		background: #1CBBB4;
	}

	.trag {
		border-radius: 15upx;
		max-width: 300px;
		position: absolute;
		top: 20px;
		left: 10px;
		width: 100px;
		height: 50px;
		background: #1CBBB4;
	}

	.close {
		position: absolute;
		right: 3px;
		top: 0px;
		right: -5px;
		top: -7px;
		color: #F43F3B;
	}
</style>
