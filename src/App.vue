<template>
	<h1> NASA IOTD </h1>
	<h3 id='date'> {{image.date}} </h3>
	<a :href='image.url' target='_blank'>
		<img :src="image.url" height='650'/>
	</a>
	<div id='button-container'>
		<button class='left' @click='getImg(randDate())'> New Image </button>
		<button class='right' @click='getImg(getDate())'> Go To Date </button>
	</div>
	<input type='date' id='date-entry'>
	<div id='explaination'>
		<h3> {{image.explanation}} </h3>
	</div>
	<div id='hd'>
		<a :href='image.hdurl'><button>Get the HD image!</button></a>
	</div>
</template>

<script>
export default {
	data() {
		return {
			image: {}
		}
	},
	mounted() {
		this.getImg()
	},
	methods: {
		async getImg (pictureDate) {
			if (pictureDate == undefined || pictureDate == "") {
				let today = new Date();
				pictureDate = today.getFullYear() + '-' + (today.getMonth() + 1) + '-' + today.getDate();
			}
			let response = await fetch('https://api.nasa.gov/planetary/apod?api_key=AkPCFO0ig2tTCxOE4U5yM0zrkp0hoBjBs0YeSB5R&date=' + pictureDate) // TODO change key
			let json = await response.json();
			this.image = json
			
		},
		getDate () {
			return document.querySelector('#date-entry').value
		},
		randDate () {
			return Math.ceil(Math.random() * 16 + 2004) + '-' + Math.ceil(Math.random() * 12) + '-' + Math.ceil(Math.random() * 28);
		}
	},
}
</script>

<style scoped>
	h1 {
		font-family: sans-serif;
		font-size: 50px;
		text-align: center;
	}

	h3 {
		font-family: sans-serif;
		font-weight: 400;
		text-align: center;
	}
	
	img {
		display: block;
		margin-left: auto;
		margin-right: auto;
	}

	#button-container {
		padding-top: 20px;
		width: 20%;
		display: block;
		margin-left: auto;
		margin-right: auto;
	}

	.right{
		float: right;
	}
	
	#date-entry {
		margin-left: auto;
		margin-right: auto;
		display: block;
	}

	h1, h3 {
		margin: 0;
		color: white;
	}

	#hd {
		width: 20%;
		text-align: center;
		margin-left: auto;
		margin-right: auto;
	}
</style>
