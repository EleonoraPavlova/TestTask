<template>
	<div :class="theme === 'light' ? 'light-theme' : 'dark-theme'">
		<div class="flex">
			<Buttons
				class="button margin-t"
				color="warning"
				size="extra-small"
				@click="changeTheme()"
				>Mood</Buttons
			>
		</div>
		<Components />
	</div>
</template>

<script>
import Components from "./components/Components.vue";
import Buttons from "./components/Buttons.vue";
export default {
	name: "App",
	components: {
		Components,
		Buttons,
	},
	data() {
		return {
			theme: "light",
		};
	},
	methods: {
		changeTheme() {
			this.theme = this.theme === "dark" ? "light" : "dark";
		},
	},
};
</script>

<style lang="scss">
</style>
