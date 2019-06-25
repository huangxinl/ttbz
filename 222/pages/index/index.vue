<template>
	<view class="banner">
		<!-- <avatar selWidth="200px" selHeight="400upx" @upload="myUpload" :avatarSrc="url" avatarStyle="width: 100%; height: 220px; border-radius:0 ">
		</avatar> -->
		<view style="text-align: center;">
			<!-- <canvas style="width: 300px; height: 200px;" canvas-id="firstCanvas"></canvas> -->
			<image :src="imgUrl" mode="" class="selectimg"></image>
			<button class="mini-btn" type="default" size="mini" @click="chooseImage">更换背景图</button>
		</view>
		<view class="cu-bar bg-white" style="min-height: 0;">
			<view class="action">
				<text class="cuIcon-titles text-green"></text>
				<text style="padding: 5px 0;">{{tip}}</text>
			</view>
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
						<view data-id="10" @click="changeColor" class="cu-tag round bg-orange light">灰</view>
						<view data-id="11" @click="changeColor" class="cu-tag round bg-olive light">灰</view>
						<view data-id="12" @click="changeColor" class="cu-tag round bg-blue light">灰</view>
					</view>
				</view>
			</view>
			<view class="btn-wrap">
				<button class="mini-btn" type="primary" size="mini" @click="handleNewFace">生成</button>
				<button class="mini-btn" type="default" size="mini" @click="addText">TEXT</button>
			</view>
			<view class="trag" :style="{top:styleCss.top,left:styleCss.left,height,width,background:styleCss.bcColor}"
			 @touchstart="start" @touchmove="move" v-if="flag" @touchend="end">
				<input type="text" class="txt-input" @blur="losefocurs" @input="handleKeUp" :style="{height,width,fontSize:styleCss.font,color:styleCss.color,background:styleCss.bcColor}" />
				<text class="lg text-gray cuIcon-roundclosefill close" @click="handleCloseClick" v-show="index"></text>
			</view>
			<text class="mytxt">sadfasdf我阿嘎是啊是</text>
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
				imgUrl: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1561454443237&di=18794bc4b583a8f4c53b563eadbd66bf&imgtype=0&src=http%3A%2F%2Fimg3.cache.netease.com%2Fphoto%2F0001%2F2010-10-14%2F6IVN5LN300AQ0001.jpg',
				index: 1,
				textInput: '',
				colorId: 0,
				url: "../../static/horse.png",
				idd: 1,
				width: '50px',
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
					top: Math.random() * 100 + 'px',
					left: Math.random() * 150 + 'px',
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
		},
		methods: {
			canvasIdErrorCallback: function(e) {
				console.error(e.detail.errMsg)
			},
			myUpload(rsp) {
				this.url = rsp.path; //更新头像方式一
				//rsp.avatar.imgSrc = rsp.path; //更新头像方式二
			},
			handleKeUp(e) {
				if (e.detail.value.length === 0) {
					e.detail.value = ' '
				}
				this.textInput = e.target.value
				let i = this.idd
				this.len = e.detail.value.length
				this.changeInput(i, this.len)
				console.log(this.len)
			},
			changeInput(i, len) {
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
						this.styleCss.color = 'yellow'
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
				this.styleCss.top = this.disY + 'px'
				this.styleCss.left = this.disX + 'px'
			},
			end(e) {},
			losefocurs(e) {
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
			chooseImage() {
				var that = this
				uni.chooseImage({
					count: 1, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: function(res) {
						let url = JSON.stringify(res.tempFilePaths)
						that.imgUrl = JSON.parse(url)[0]
					}
				});
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
		src: url('https://code.z01.com/font/ZoomlaXingtiJ.eot?#iefix') format("embedded-opentype"),
			url('https://code.z01.com/font/ZoomlaXingtiJ.woff') format("woff"),
			url('https://code.z01.com/font/ZoomlaXingtiJ.ttf') format("truetype"),
			url('https://code.z01.com/font/ZoomlaXingtiJ.svg#ZoomlaXingtiJ') format("svg");
		font-style: normal;
		font-weight: normal;
	}

	.btn-wrap {
		display: flex;
		flex-direction: row;
		justify-content: center;
	}
	.selectimg {
		width: 100%;
	}

	.banner {
		width: 100%;
		overflow: hidden;
	}


	.select {
		height: 40upx;
		line-height: 40upx;
	}

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

	.text-xl {}

	.text {
		position: relative;
		top: 0;
		left: 5px;
		margin: 5px 0;
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
		color: #000000;
		border-radius: 50%;
		font-size: 20upx;
	}

	.text-color {
		flex: 0 0 150upx;
		font-size: 30upx;
		margin-left: 5px;
	}

	.container {
		display: flex;
		align-items: center;
	}

	.cont {
		flex: 1;
	}

	.content {
		padding: 20px 0 0;

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
		font-family: ZoomlaXingtiJ!important;
		border-radius: 15upx;
		background: #fff;
		text-align: center;
	}
	
	.mytxt {
		font-family: 'ZoomlaXingtiJ';
	}
	.picture {
		text-align: center;
	}


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
