<template lang="pug">
div
	header.bg-green
		row(center)
			column(small="1", medium="2:3")
				h3.logo lists
	main.bg-white
		<nuxt></nuxt>
	svd-footer
</template>
<style lang="scss">
@import "~svd-style/ext";
header {
  padding: grid(1);
  @media #{$small-only} {
    height: 80px;
    padding: 0 30px;
  }
  h3 {
    line-height: 80px;
  }
}
</style>
<script>
import svdFooter from "svd-footer/src/components/svd-footer.vue";

export default {
  components: { svdFooter }
};
</script>
