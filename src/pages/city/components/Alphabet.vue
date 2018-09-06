<template lang="html">
  	<ul class="list">
		<li class="item"
			v-for="(item,index) in letters"
			:key = "item"
			:ref="item"
			@touchstart.prevent = "handleTouchStart"
			@touchmove = "handleTouchmove"
			@touchend = "handleTouchend"
			@click="handleLetterClick"
		>
		{{item}}</li>
  	</ul>
</template>

<script>
export default {
	name:'CityAlphabet',
	props:{
		cities:Object
	},
	computed:{
		letters(){
			const letters = []
			for (let key in this.cities) {
				letters.push(key)
			}
			return letters
		}
	},
	data () {
		return{
			touchStatus: false,
			startY:0,
			timer:null
		}
	},
	updated(){
		// A 距离头部最下面的高度
		this.startY  = this.$refs['A'][0].offsetTop
	},
	methods:{
		handleLetterClick(e){
			this.$emit('change',e.target.innerText)
			console.log('改变',e.target.innerText)
		},
		handleTouchStart (){
			this.touchStatus = true
		},
		handleTouchmove (e){
			if (this.touchStatus) {
				// 触摸的元素距离头部顶部的距离   头部 79
				if( this.timer) {
					clearTimeout(this.timer)
				}
				this.timer = setTimeout( () => {
					const touchY = e.touches[0].clientY - 79
					const index = Math.floor((touchY - this.startY) / 20)
					if ( index >=0 && index < this.letters.length){
						this.$emit('change',this.letters[index])
					}
				},16)
			}
		},
		handleTouchend (){
			this.touchStatus = false
		}
	}
}
</script>

<style lang="stylus" scoped>
	@import '~styles/varibles.styl'
	.list
		display: flex
		flex-direction: column
		justify-content: center
		position: absolute
		top: 1.58rem
		right: 0
		bottom: 0
		width: .4rem
		.item
			line-height: .44rem
			text-align: center
			color: $bgColor

</style>
