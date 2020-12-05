<template>
	<div id="top">
		<h1> NASA IOTD </h1>
		<h3 id='date'> {{object.date}} </h3>
	</div>
</template>

<script>
export default {
	props: ['object'],
	methods: {

	},
}
</script>

<style scoped>
	* {
		font-family: sans-serif;
		text-align: center;
	}

	h1 {
		font-size: 40px;
	}

	h3 {
		font-size: 25px;
	}

	h1, h3 {
		margin: 0;
		color: white;
	}

	#top {
		background-color: #134;
		margin-bottom: 20px;
		border: 4px solid #cde;
		width: 95vw;
		display: block;
		margin-left: auto;
		margin-right: auto;
	}
</style>