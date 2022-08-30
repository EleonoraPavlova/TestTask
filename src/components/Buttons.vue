<template>
	<button
		class="button margin-l"
		:class="[color, size]"
		@click="$emit('click')"
	>
		<slot />
	</button>
</template>

<script >
export default {
	name: "Buttons",
	props: {
		color: {
			type: String,
			default: "primary",
		},
		size: {
			type: String,
			default: "big",
		},
	},
	emits: ["click"],
};
</script>

<style lang="scss">
.button {
	border-radius: 10px;
	border: none;
	padding: 12px;
	width: 15%;
	outline: none;
	opacity: 0.8;
	&.midl {
		font-size: 14px;
		padding: 4px 8px;
		height: 26px;
	}
	&.small {
		font-size: 14px;
		padding: 3px 6px;
		min-width: 54px;
		height: 26px;
	}
	&.big {
		font-size: 20px;
		padding: 8px 16px;
	}
	&.primary {
		background-color: green;
		color: #fff;
	}
	&.danger {
		background-color: red;
		color: #fff;
	}
	&.warning {
		background-color: #ffb841;
		color: #fff;
	}
	&:hover {
		opacity: 0.6;
	}
}
</style>