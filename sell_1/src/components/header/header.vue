<template>
	<div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img width="64" height="64" :src="seller.avatar" :alt="seller.description">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div v-if="seller.supports" class="support">
					<span class="icon" :class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{seller.supports[0].description}}</span>
				</div>
			</div>
			<div v-if="seller.supports" class="support-count" @click="showDetail">
				<span class="count">{{seller.supports.length}}个</span>
				<i class="icon-keyboard_arrow_right"></i>
			</div>
		</div>
		<div class="bulletin-wrapper">
			<span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
			<i class="icon-keyboard_arrow_right"></i>
		</div>
		<div class="background">
			<img :src="seller.avatar" alt="" width="100%" height="100%">
		</div>
		<div class="detail" v-show="detailShow" transition="fade">
			<div class="detail-wrapper clearfix">
				<div class="detail-main">
					<h1 class="name">{{seller.name}}</h1>
					<div class="star-wrapper">
						<star :size="48" :score="seller.score"></star>
					</div>
					<div class="title">
						<div class="line border-1px"></div>
						<div class="text">优惠信息</div>
						<div class="line border-1px"></div>
					</div>
					<ul v-if="seller.supports" class="supports">
						<li class="support-item" v-for="item in seller.supports">
							<span class="icon" :class="classMap[item.type]"></span>
							<span class="text">{{item.description}}</span>
						</li>
					</ul>
					<div class="title">
						<div class="line border-1px"></div>
						<div class="text">商家公告</div>
						<div class="line border-1px"></div>
					</div>
					<div class="bulletin">
						<p class="content">{{seller.bulletin}}</p>
					</div>
				</div>
			</div>
			<div class="detail-close" @click="hideDetail">
				<i class="icon-close"></i>
			</div>
		</div>
	</div>
</template>

<script>
	import star from '../star/star';

	export default {
		props: {
			seller: {
				type: Object
			}
		},
		data () {
			return {
				detailShow: false
			};
		},
		components: {
			star: star
		},
		methods: {
			showDetail () {
				this.detailShow = true;
			},
			hideDetail () {
				this.detailShow = false;
			}
		},
		created () {
			this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
		}
	};
</script>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/mixin.styl";

	.header
		position: relative
		overflow: hidden
		color: #fff
		background-color: rgba(7,17,27,.5)
		.content-wrapper
			position: relative
			padding: 24px 12px 18px 24px
			font-size: 0
			.avatar
				display: inline-block
				vertical-align: top
				img
					border-radius: 2px
			.content
				display: inline-block
				margin-left: 16px
				.title
					margin: 2px 0 8px 0
					.brand
						display: inline-block
						vertical-align: top
						width: 30px
						height: 18px
						bg-image('brand')
						background-size: 30px 18px
						background-repeat: no-repeat
					.name
						margin-left: 6px
						font-size: 16px
						line-height: 18px
						font-weight: bold
				.description
					margin-bottom: 10px
					line-height: 12px
					font-size: 12px
				.support
					.icon
						display: inline-block
						vertical-align:top
						margin-right: 4px
						width: 12px
						height: 12px
						background-size: 12px 12px
						background-repeat: no-repeat
						&.decrease
							bg-image('decrease_1')
						&.discount
							bg-image('discount_1')
						&.guarantee
							bg-image('guarantee_1')
						&.invoice
							bg-image('invoice_1')
						&.special
							bg-image('special_1')
					.text
						line-height: 12px
						font-size: 10px
			.support-count
				position: absolute
				right: 12px
				bottom: 14px
				padding: 0 8px
				height: 24px
				line-height: 24px
				border-radius: 14px
				background-color: rgba(0,0,0,.2)
				text-aligh: center
				.count
					vertical-align: top
					font-size: 10px
				.icon-keyboard_arrow_right
					margin-left: 2px
					line-height: 24px
					font-size: 10px
		.bulletin-wrapper
			position: relative
			height: 28px
			line-height: 28px
			padding: 0 22px 0 12px
			white-space: nowrap
			overflow: hidden
			text-overflow: ellipsis
			background-color: rgba(7,17,27,.2)
			.bulletin-title
				display: inline-block
				vertical-align: top
				margin-top: 8px
				width: 22px
				height: 12px
				bg-image('bulletin')
				background-size: 22px 12px
				background-repeat: no-repeat
			.bulletin-text
				margin: 0 4px
				font-size: 10px
			.icon-keyboard_arrow_right
				position: absolute
				right: 12px
				top: 8px
				font-size: 10px
		.background
			position: absolute
			top: 0
			left: 0
			width: 100%
			height: 100%
			z-index: -1
			filter: blur(10px)
			
		.detail
			position: fixed
			top: 0
			left: 0
			z-index: 100
			width: 100%
			height: 100%
			overflow: auto
			backdrop-filter: blur(10px)
			transition: all 0.5s
			&.fade-transition
				opacity: 1
				background-color: rgba(7,17,27,.8)
			&.fade-enter,&.fade-leave
				opacity: 0
				background-color: rgba(7,17,27,0)
			.detail-wrapper
				width: 100%
				min-height: 100%
				.detail-main
					margin-top: 64px
					padding-bottom: 64px
					.name
						line-height: 16px
						text-align: center
						font-size: 16px
						font-weight: 700
					.star-wrapper
						margin-top: 16px
						padding: 2px 0
						text-align: center
					.title
						display: flex
						width: 80%
						margin: 28px auto 24px
						.line
							flex: 1
							position: relative
							top -6px
							border-bottom: 1px solid rgba(255,255,255,.2)
						.text
							padding: 0 12px
							font-size: 14px
							font-weight: 700
					.supports
						width: 80%
						margin: 0 auto
						font-size: 0
						.support-item
							padding: 0 12px
							margin-bottom: 12px
							&:last-child
								margin-bottom: 0
							.icon
								display: inline-block
								margin-right: 6px
								vertical-align: top
								width: 16px
								height: 16px
								background-size: 16px 16px
								background-repeat: no-repeat
								&.decrease
									bg-image('decrease_2')
								&.discount
									bg-image('discount_2')
								&.guarantee
									bg-image('guarantee_2')
								&.invoice
									bg-image('invoice_2')
								&.special
									bg-image('special_2')
							.text
								line-height: 16px
								font-size: 12px
					.bulletin
						width: 80%
						margin: 0 auto
						.content
							padding: 0 12px
							line-height: 24px
							font-size: 12px
								
			.detail-close
				position: relative
				width: 32px
				height: 32px
				margin: -64px auto 0 auto
				clear: both
				font-size: 32px
				color: rgba(255,255,255,.5)
					
</style>
