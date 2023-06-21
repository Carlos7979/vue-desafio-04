<script>
	import Header from './components/Header.vue'
	import Info from './components/Info.vue'

	export default {
		components: {
			Header,
			Info,
		},
		data() {
			return {}
		},
		created() {},
		methods: {},
		computed: {}
	}
</script>

<template>
	<Header></Header>
	<div class="main">
		<Info></Info>
		<hr />
	</div>
</template>

<style scoped>

</style>
