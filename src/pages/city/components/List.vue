<template lang="html">
	<div class="list" ref="wrapper">
		<div class="">
			<div class="area">
				<div class="title border-topbottom">当前城市</div>
				<div class="button-list">
					<div class="button-wrapper">
						<div class="button">{{city}}</div>
					</div>
				</div>
			</div>
			<div class="area">
				<div class="title border-topbottom">热门城市</div>
				<div class="button-list">
					<div class="button-wrapper" v-for="(item,index) in hot" :key="item.id" @click="handleCityClick(item.name)">
						<div class="button">{{item.name}}</div>
					</div>
				</div>
			</div>
			<div class="area"
				v-for="(item,key,index) in cities"
				:key="key"
				:ref="key"
			>
				<div class="title border-topbottom">{{key}}</div>
				<div class="item-list">
					<div class="item border-bottom" v-for="cityItem in item" :key="cityItem.id" @click="handleCityClick(cityItem.name)">{{cityItem.name}}</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import {mapState, mapMutations} from 'vuex'
import Bscroll from "better-scroll"
export default {
	name: 'cityList',
	props:{
		cities:Object,
		hot:Array,
		letter:String
	},
	computed:{
		...mapState(['city'])
	},
	created(){
		console.log(this.hot)
	},
	methods:{
		handleCityClick(cityName){
			console.log(cityName)
			// this.$store.dispatch('change',cityName)
			this.CHANGE(cityName)
			this.$router.push('/')
		},
		...mapMutations(['CHANGE'])
	},
	mounted(){
		this.scroll = new Bscroll(this.$refs.wrapper,{ mouseWheel: true, click: true, tap: true })
	},
	watch:{
		letter() {
			if(this.letter){
				const element = this.$refs[this.letter][0]
				this.scroll.scrollToElement(element)
			}
		}
	}
}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.border-topbottom
		&:before
			border-color: #ccc
		&:after
			border-color: #ccc
	.border-bottom
		&:before
			border-color: #ccc
	.list
		overflow: hidden
		position: absolute
		top: 1.58rem
		left: 0
		right: 0
		bottom: 0
		.title
			line-height: .54rem
			background: #eee
			padding-left: .2rem
			color: #666
		.button-list
			padding: .1rem .6rem .1rem .1rem
			overflow: hidden
			.button-wrapper
				float: left
				width: 33.33%
				.button
					margin: .1rem
					padding: .1rem 0
					text-align: center
					border: .02rem solid #ccc
					border-radius: .06rem
		.item-list
			.item
				line-height: .76rem
				color: #666
				padding-left: .2rem
</style>
