<template lang="html">
	<div class="">
		<home-header></home-header>
		<home-swiper :list="swiperList"></home-swiper>
		<home-icons :list="iconList"></home-icons>
		<home-recommend :list= "recommendList"></home-recommend>
		<home-weekend :list = "weekendList"></home-weekend>
	</div>
</template>

<script>
import {mapState} from 'vuex'
import homeHeader from './components/Header'
import homeSwiper from './components/Swiper'
import homeIcons from './components/Icons'
import homeRecommend from './components/Recommend'
import homeWeekend from './components/Weekend'
import axios from 'axios'
export default {
	name: 'Home',
	components:{
		homeHeader,
		homeSwiper,
		homeIcons,
		homeRecommend,
		homeWeekend
	},
	data () {
		return{
			lastCity:'',
			swiperList:[],
			iconList:[],
			recommendList:[],
			weekendList:[]
		}
	},
	computed:{
			...mapState(['city'])
	},
	methods:{
		getHomeInfo(){
			axios.get('/api/index.json?'+this.city)
			.then(this.getHomeInfoSucc)
		},
		getHomeInfoSucc(res){
			res = res.data;
			if(res.ret && res.data){
				const data = res.data;
				// this.city = data.city;
				this.swiperList = data.swiperList;
				this.iconList = data.iconList;
				this.recommendList = data.recommendList;
				this.weekendList = data.weekendList
			}
			console.log(res)
		}
	},
	mounted (){
		this.lastCity = this.city
		this.getHomeInfo()
	},
	activated () {
      if (this.lastCity !== this.city) {
        this.lastCity = this.city
        this.getHomeInfo()
      }
    }
}
</script>

<style lang="css">
</style>
