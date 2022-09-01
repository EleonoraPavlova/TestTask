<template>
	<h1 class="bold pagb" :style="changeStyle">
		{{ title }}
	</h1>
</template>

<script>
export default {
	name: "H1Title",
	props: {
		title: {
			type: String,
			default: "List notes",
		},
		color: {
			type: String,
			default: "red",
		},
		fontSize: {
			type: String,
			default: "2rem",
		},
	},

	computed: {
		changeStyle() {
			return {
				color: this.color,
				fontSize: this.fontSize,
			};
		},
	},
};
</script>

<style>
</style>