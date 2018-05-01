<template lang="pug">
div
	header
		row(center)
			column(small="1", medium="2:3")
				h3.logo lists
	main.bg-white
		<nuxt></nuxt>
</template>
<style>
</style>

<script>
import headings from '~/static/head.json';
// import Footer from 'svd-footer'


export default{
	head: headings
}
</script>
