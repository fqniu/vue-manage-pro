<template>
	<div class="world_wrap">
		<World />
	</div>
</template>

<script>
import World from "./chart/World.vue";
export default {
	name: 'Echarts3',
	data () {
		return {
		};
	},
	methods: {},
	components: {
		World
	},
}

</script>
<style  lang="scss" scoped>
.world_wrap{
	width: 100%;
	height: 100%;
}
</style>
