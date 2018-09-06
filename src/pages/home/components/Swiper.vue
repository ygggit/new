<template lang="html">
	<div class="wrapper">
		<swiper :options="swiperOption" v-if="showSwiper">
			<swiper-slide v-for="(item,index) in list" :key="index">
				<img :src="item.imgUrl" class="swiper-img" />
			</swiper-slide>
			<div class="swiper-pagination"  slot="pagination"></div>
		</swiper>
	</div>
</template>

<script>
export default {
	name:'HomeSwiper',
	props: {
      list: Array
    },
	data() {
		return{
			swiperOption:{
				pagination: {
					 el: '.swiper-pagination'
				},
				// autoplay:true,
				loop:true
			}
		}
	},
	computed: {
		showSwiper(){
			return this.list.length
		}
	}

}
</script>

<style lang="stylus" scoped>
	.wrapper >>> .swiper-pagination-bullet-active
		background: #fff
	.wrapper
		width: 100%;
		height: 0
		overflow: hidden
		padding-bottom: 31.25%
		background:	#ccc
		.swiper-img
			width: 100%


</style>
