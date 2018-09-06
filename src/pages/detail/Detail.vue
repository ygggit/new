<template lang="html">
	<div class="">
		<detail-banner :sightName="sightName" :bannerImg="bannerImg" :gallaryImgs="gallaryImgs"></detail-banner>
		<detail-Header></detail-Header>
		<div class="container" style="height:50rem">
			<detail-list :list="list"></detail-list>
		</div>
	</div>
</template>

<script>
import detailBanner from './components/Banner.vue'
import detailHeader from './components/Header.vue'
import detailList from './components/List.vue'
import axios from 'axios'
export default {
	name: 'Detail',
	components:{
		detailBanner,
		detailHeader,
		detailList
	},
	data () {
		return {
			sightName:'',
			bannerImg:'',
			gallaryImgs: [],
			list: []
		}
	},
	methods:{
		getDetailInfo () {
			axios.get('/api/detail.json',{
				params:{id:this.$route.params.id}
			}).then(this.getDetailInfoSucc)
		},
		getDetailInfoSucc (res) {
			if ( res.data.ret && res.data.data){
				const data = res.data
				this.sightName = data.data.sightName
				this.bannerImg = data.data.bannerImg
				this.gallaryImgs = data.data.gallaryImgs
				this.list = data.data.categoryList
			}
		}
	},
	mounted(){
		this.getDetailInfo()
	}
}
</script>

<style lang="stylus" scoped="">
</style>
