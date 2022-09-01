.<template>
	<input
		:value="modelValue"
		class="container__main_input"
		type="text"
		@input="updateInput"
	/>
	<!--:placeholder="placeholderString" - bind забаиндили динамич значение 
	@input="inputChangeHandler" вызываем слушатель события, функцию -->
</template>
<script>
export default {
	name: "Input",
	props: {
		modelValue: {
			type: String,
			default: "",
		},
	},
	emits: ["update:modelValue"],
	methods: {
		updateInput(event) {
			this.$emit("update:modelValue", event.target.value);
		},
	},
};
</script>

<style scoped>
</style>