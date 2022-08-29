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
						@keydown.enter="addHewNote"
						@input="inputChangeHandler"
					/>
					<!--:placeholder="placeholderString" - bind забаиндили динамич значение 
					@input="inputChangeHandler" вызываем слушатель события, функцию -->
					<button class="container__main_button margin-l" @click="addHewNote">
						Add
					</button>
				</div>
			</div>
			<hr class="container__hr" />
			<ul class="flex">
				<li v-for="note in notes" :key="note">{{ note }}</li>
			</ul>
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
			notes: ["notes 1", "notes 2", "notes 3"],
		};
	},
	methods: {
		inputChangeHandler(event) {
			// console.log("inputChangeHandler",event.target.value );
			this.inputValue = event.target.value;
			//2х сторонее связывание закончили
		},
		addHewNote() {
			//добавляем новую заметку в массив notes
			this.notes.push(this.inputValue);
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
	&__hr {
		text-align: center;
		margin: 35px;
	}
}
</style>