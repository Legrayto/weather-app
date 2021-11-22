<template>
  <div id="app" class='p-6 wrapper has-background-info'>
		<div class="columns mb-2 ">
			<div class="column is-half is-offset-3">
				<div class="field has-addons">
					<div class="control is-expanded">
						<input
							type="text"
							v-model='search'
							@keypress.enter='queryWeather'
							class="input"
						>
					</div>
					<div class="control">
						<button @click='queryWeather' class="button is-success">Click</button>
					</div>
				</div>
			</div>
		</div>

		<div class="columns" v-if='Object.keys(weather).length > 0'>
			<div class="column is-8 is-offset-2">
				<div class="tile is-ancestor">
					<div class="tile is-parent is-vertical">
						<article class="tile is-child notification is-white">
							<p class="title">{{getDate()}}</p>
						</article>
						<article class="tile is-child notification is-white">
							<p class="title">{{weather.weather[0].main}}</p>
						</article>
					</div>
					<div class="tile is-parent">
						<article class="tile is-child notification is-white">
							<p class="title">{{Math.round(kelvin)}}°c</p>
							<div class='subtitle'>
								<div class=''>{{weather.name}}</div>
								<div class=''>{{weather.sys.country }}</div>
							</div>
						</article>
					</div>
				</div>
		</div>
		</div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {},

	data() {
		return {
			apiKey: '107cc48e9f75daa7f39732002fb421f5',
			url: 'https://api.openweathermap.org/data/2.5/',
			search: '',
			weather: {}
		}
	},

	methods: {
		queryWeather() {
			fetch(`${this.url}weather?q=${this.search}&appid=${this.apiKey}&lang=ru`)
			.then(res => res.json())
			.then(res => {this.weather = res
       console.log(`${this.url}weather?q=${this.search}&appid=${this.apiKey}`)
      })
		},

		getDate () {
      let date = new Date();
      return `${date.getDate()}.${date.getMonth()}.${date.getFullYear()}`;
    }
	},

	computed: {
		kelvin() {
			return  this.weather.main.temp - 273.15
		}
	}

}
</script>

<style>
.wrapper {
	height: 100vh;
}
</style>
