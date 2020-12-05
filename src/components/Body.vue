<template>
  <a :href='object.url' target='_blank' v-if='object.objectType === "vid"'>
		<iframe :src='object.url'></iframe>
	</a>
	<a :href='object.url' target='_blank' v-else>
		<img :src="object.url" height='600'/>
	</a>
	<div id='button-container'>
		<button class='left' @click='getImg(randDate())'> New picture</button>
		<button class='right' @click='getImg(getDate())'> Go To Date </button>
	</div>
	<input type='date' id='date-entry'>
	<div id='explaination'>
		<h3> {{object.explanation}} </h3>
	</div>
	<div id='hd' v-if="object.objectType === 'img'">
		<a :href='object.hdurl'><button>Get the HD image!</button></a>
	</div>
</template>

<script>
export default {
	emits: ['update-obj'],
	data () {
		return {
			object: {}
		}
	},
	methods: {
		async getImg (pictureDate) {
			if (pictureDate == undefined || pictureDate == "") {
				let today = new Date();
				pictureDate = today.getFullYear() + '-' + (today.getMonth() + 1) + '-' + today.getDate();
			}
			let response = await fetch('https://api.nasa.gov/planetary/apod?api_key=AkPCFO0ig2tTCxOE4U5yM0zrkp0hoBjBs0YeSB5R&date=' + pictureDate) // TODO change key
			let json = await response.json();
			let extension = json.url.split('.')
			this.object = json

			if (extension.indexOf('youtube') != -1) {
				this.object.objectType = 'vid'
				console.log('this is a video')
			} else {
				this.object.objectType = 'img'
				console.log('this is an image')
			}

			this.$emit('update-obj', this.object)
		},
		getDate () {
			return document.querySelector('#date-entry').value
		},
		randDate () {
			return Math.ceil(Math.random() * 16 + 2004) + '-' + Math.ceil(Math.random() * 12) + '-' + Math.ceil(Math.random() * 28);
		}
	},
	mounted () {
		this.getImg()
	}
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

    h1, h3 {
		margin: 0;
		color: white;
	}

	iframe {
		border: 5px solid #cde;
		height: 66vh;
		width: 95vw;
		margin-left: auto;
		margin-right: auto;
		display: block;
	}

    #button-container {
		padding-top: 20px;
		width: 20%;
		display: block;
		margin-left: auto;
		margin-right: auto;
	}

    #date-entry {
		margin-left: auto;
		margin-right: auto;
		display: block;
	}

	#hd {
		width: 20%;
		text-align: center;
		margin-left: auto;
		margin-right: auto;
	}

    .right{
		float: right;
	}
</style>