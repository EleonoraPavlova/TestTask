<template>
	<div class="container">
		<div class="container-box">
			<H1Title
				:color="inputValue.length < 5 ? 'chocolate' : 'green'"
				:font-size="inputValue.length < 5 ? '2rem' : '1.5rem'"
			/>
			<div class="flex-center">
				<div class="container__main">
					<Input
						v-model="inputValue"
						:placeholder="placeholderString"
						@keypress.enter="addNewNote"
					/>
					<Buttons color="primary" @click="addNewNote">Add</Buttons>
				</div>
			</div>
			<hr class="container__hr" />
			<ul v-if="notes.length !== 0" class="flex container__ul">
				<li
					v-for="(note, index) in notes"
					:key="note"
					class="flex-between container__item"
				>
					<!-- <span :class="note.length > 5 ? 'green' : 'bold'">
						{{ index + 1 }}, {{ toUpperCase(note) }}</span
					> -->
					<!-- <span :class="{ green: true, bold: note.length > 5 }">
						{{ index + 1 }}, {{ toUpperCase(note) }}</span
					> -->
					<span :class="['bold', { green: note.length > 5 }]">
						{{ index + 1 }}, {{ toUpperCase(note) }}</span
					>

					<Buttons
						class="button"
						size="small"
						color="warning"
						@click="deleteNote(index)"
						>Delete</Buttons
					>
				</li>

				<li>
					<h4 class="bold">Total: {{ notes.length }}</h4>
					double : {{ doubleCount }}
				</li>
			</ul>
			<div v-if="notes.length === 0">No notes, add first note please</div>
			<hr class="container__hr" />
			<h4 v-once class="margin">{{ title }}</h4>
			<h4 v-pre class="margin">{{ title }}</h4>
			<div class="flex-center margin">
				<h4 v-text="title" />
				<Buttons
					class="button"
					size="small"
					color="primary"
					@click="title = 'I am another title'"
					>Change title
				</Buttons>
			</div>
			<hr class="container__hr" />
			<ArrayNumbers />
			<hr class="container__hr" />
			<ul class="flex-center container__ul">
				<!-- v-for="value in person" итерация по обьектам -->
				<li
					v-for="(value, key) in person"
					:key="value"
					class="margin-l container__item"
				>
					{{ key }}:
					<strong> {{ value }}</strong>
				</li>
			</ul>
			<hr class="container__hr" />
			<div class="margin">
				<Input
					ref="myInput"
					:placeholder="placeholderString1"
					@keyup.enter="addNumber($event)"
				/>
			</div>
			<ul class="container__ul">
				<!-- v-for="value in person" итерация по обьектам -->
				<li
					v-for="(number, index) in evenNumbers"
					:key="number"
					class="margin-l container__item"
					@click="deleteNumber(index), log(item)"
				>
					<strong> {{ number }}</strong
					>&nbsp;
					<Input @click.stop />
				</li>
			</ul>
			<div v-show="numbers.length === 0">
				Oops........ You deleted all numbers
			</div>
		</div>
	</div>
</template>

<script>
import Buttons from "./Buttons.vue";
import Input from "./Input.vue";
import H1Title from "./H1Title.vue";
import ArrayNumbers from "./ArrayNumbers.vue";
export default {
	name: "Components",
	components: {
		Buttons,
		Input,
		H1Title,
		ArrayNumbers,
	},
	data() {
		//данные, которые есть в нашем приложении
		return {
			inputValue: "",
			placeholderString: "Enter the note",
			placeholderString1: "Enter something.....",
			title: "List notes",
			notes: ["note 1", "note 2", "note 3"],
			person: {
				firstName: "Eleonora",
				lastName: "Pavlova",
				age: 31,
			},
			numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9],
		};
	},
	computed: {
		doubleCount() {
			console.log("doubleCount");
			return this.notes.length * 2;
		},
		// выводим только четные
		evenNumbers() {
			return this.numbers.filter((i) => i % 2 === 0);
		},
	},
	watch: {
		inputValue(value) {
			if (value.length > 20) {
				this.inputValue = "";
			}
			console.log("input value changed", value);
		},
	},
	methods: {
		addNewNote() {
			//добавляем новую заметку в массив notes
			// if (this.inputValue !== "") чтобы не добавлялся пустой пост
			if (this.inputValue !== "") {
				this.notes.push(this.inputValue);
				this.inputValue = "";
			}
		},

		toUpperCase(item) {
			return item.toUpperCase();
		},
		addNumber(event) {
			//вообще это если доступ нужен к html, не к компоненте
			this.numbers.unshift(this.$refs.myInput.value);
			this.$refs.myInput.value = "";
			console.log(event.key);
		},
		// inputKeyPress(event) {
		// 	//функц, чтобы узнать какая кнопка была нажата пользователем
		// 	console.log(event.key);
		// 	if (event.key === "Enter") {
		// 		this.addNewNote();
		// 	}
		// },
		deleteNote(index) {
			this.notes.splice(index, 1);
		},
		deleteNumber(index) {
			this.numbers.splice(index, 1);
			// this.inputValue = "";
		},
		// чтобы не было удаление по клику от родителя или пишем на элемент @click.stop
		stopPropagation(event) {
			event.stopPropagation();
		},
		log(item) {
			console.log("Log item:", item);
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
	}
	&__hr {
		text-align: center;
		margin: 35px;
	}
	&__ul {
		padding: 0 20px;
		margin: 0 35px;
	}
	&__item {
		margin-bottom: 20px;
	}
}
</style>