<template lang="html">
	<div>
		<city-header></city-header>
		<city-search :cities = "cities"></city-search>
		<city-list :cities = "cities" :hot="hotCities" :letter="letter"></city-list>
		<city-alphabet :cities="cities" @change="handeleLetterChange"></city-alphabet>
	</div>
</template>

<script>
import axios from 'axios'
import cityHeader from './components/Header.vue'
import citySearch from './components/Search.vue'
import cityList from './components/List.vue'
import cityAlphabet from './components/Alphabet.vue'
export default {
	name: "City",
	components:{
		cityHeader,
		citySearch,
		cityList,
		cityAlphabet
	},
	data(){
		return{
			hotCities:[],
			cities:{},
			letter:''
		}
	},
	methods:{
		getCityInfo (){
			axios.get('/api/city.json')
			.then(this.headerGetCityInfoSucc)
		},
		headerGetCityInfoSucc(res){
			res = res.data;
			if(res.ret && res.data){
				const data = res.data
				this.hotCities = data.hotCities
				this.cities = data.cities
				console.log('this.hotCities',this.hotCities)
			}
		},
		handeleLetterChange(letter){
			console.log('获取',letter)
			this.letter = letter
		}
	},
	mounted(){
		this.getCityInfo()
	}
}
</script>

<style lang="stylus" scoped>
</style>
