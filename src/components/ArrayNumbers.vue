<template>
	<ul class="flex-row container__ul">
		<li
			v-for="(item, index) in 15"
			:key="item"
			class="flex-between container__item"
		>
			<strong>{{ index }}:</strong>{{ item }}
		</li>
	</ul>
</template>

<script>
export default {
	name: "ArrayNumbers",
};
</script>

<style>
</style>