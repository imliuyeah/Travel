<template>
	<div>
		<city-header></city-header>	
		<city-search :cities="cities"></city-search>
		<city-list :hotCities="hotCities" :cities="cities" :letter="letter"></city-list>
		<city-alphabet :cities="cities" @change="handleLetterChange"></city-alphabet>
	</div>
</template>

<script>
	import CityHeader from './components/Header.vue'
	import CitySearch from './components/Search.vue'
	import CityList from './components/List.vue'
	import CityAlphabet from './components/Alphabet.vue'
	import axios from 'axios'

	export default {
		components: {
			CityHeader,
			CitySearch,
			CityList,
			CityAlphabet
		},
		data () {
			return {
				hotCities: [],
				cities: {},
				letter: ''
			}
		},
		methods: {
			getCityInfo (){
				axios.get('/static/mock/city.json')
					.then(this.getCityInfoSucc)
			},
			getCityInfoSucc (res) {
				res = res.data
				if(res.ret && res.data) {
					const data = res.data
					this.hotCities = data.hotCities
					this.cities = data.cities
				}
			},
			handleLetterChange (letter) {
				this.letter = letter
			}
		},
		mounted (){
			this.getCityInfo()
		}

	}
</script>

<style>
	
</style>