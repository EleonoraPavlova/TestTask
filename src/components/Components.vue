<template>
	<div class="container">
		<div class="container-box">
			<h1 class="bold pagb">{{ title }}</h1>
			<div class="flex-center">
				<div class="container__main">
					<input
						class="container__main_input"
						:value="inputValue"
						:placeholder="placeholderString"
						type="text"
						@input="inputChangeHandler"
					/>
					<!--:placeholder="placeholderString" - bind забаиндили динамич значение 
					@input="inputChangeHandler" вызываем слушатель события, функцию -->
					<button class="container__main_button margin-l">Add</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "Components",
	data() {
		//данные, которые есть в нашем приложении
		return {
			placeholderString: "Enter the note",
			title: "List notes",
			inputValue: "",
		};
	},
	methods: {
		inputChangeHandler(event) {
			// console.log("inputChangeHandler",event.target.value );
			this.inputValue = event.target.value;
			//2х сторонее связывание закончили
		},
	},
};
</script>

<style scoped lang="scss">
.container {
	padding: 50px;
	&__main {
		display: flex;
		justify-content: center;
		width: 70%;
		&_input {
			padding: 10px;
			width: 55%;
		}
		&_button {
			background-color: transparent;
			border: 1px solid green;
			border-radius: 5px;
			padding: 12px;
			width: 15%;
			&:hover {
				background-color: lightgreen;
				opacity: 0.8;
			}
		}
	}
}
</style>