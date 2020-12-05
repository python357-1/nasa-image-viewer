<template>
	<Header v-bind:object='object' ></Header>
	<Body @update-obj='updateObject($event)'></Body>
</template>

<script>
import Header from './components/Header.vue'
import Body from './components/Body.vue'

export default {
	components: { Header, Body },
	data () {
		return {
			object: {}
		}
	},
	methods: {
		updateObject(obj) {
			this.object = obj;
		}
	}
}
</script>

<style scoped>
</style>
