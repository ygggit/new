<template lang="html">
	<div class="">
		<div class="recommend-title">周末去哪儿</div>
		<ul>
			<li class="item" v-for = "(item,index) in list" :key="item.id">
				<div class="item-img-wrapper">
					<img class="item-img" :src="item.imgUrl" alt="">
				</div>
				<div class="item-info">
					<p class="item-title">{{item.title}}</p>
					<p class="item-desc">{{item.desc}}</p>
				</div>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: 'homeWeekend',
	props:{
		list:Array
	},
	data () {
		return {}
	}
}
</script>

<style lang="stylus" scoped>
	@import '~styles/mixins.styl'
	.recommend-title
		margin-top: .2rem
		line-height: .8rem
		background: #eee
		text-indent: .2rem
	.item
		overflow: hidden
		.item-img-wrapper
			overflow: hidden;
			height: 0;
			padding-bottom: 37.09%;
			.item-img
				width: 100%
		.item-info
			padding: 0.1rem;
			.item-title
				line-height: 0.54rem
				font-size: 0.32rem
				ellipsis()
			.item-desc
				line-height: .44rem
				color: #ccc
				ellipsis()
</style>
