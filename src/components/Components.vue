<template>
	<div class="container">
		<div class="container-box">
			<h1
				class="bold pagb"
				:style="{
					color: inputValue.length < 5 ? 'red' : 'green',
					fontSize: inputValue.length < 10 ? '2rem' : '1.5rem',
				}"
			>
				{{ title }}
			</h1>
			<div class="flex-center">
				<div class="container__main">
					<input
						v-model="inputValue"
						type="text"
						class="container__main_input"
						:placeholder="placeholderString"
						@keypress.enter="addNewNote"
					/>
					<!--:placeholder="placeholderString" - bind забаиндили динамич значение 
					@input="inputChangeHandler" вызываем слушатель события, функцию -->
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
						color="danger"
						@click="deleteNote(index)"
						>Delete</Buttons
					>
				</li>

				<li>
					<h4 class="bold">Total: {{ notes.length }}</h4>
					double : {{ doubleCount }}
				</li>
			</ul>
			<hr class="container__hr" />
			<h4 v-once class="margin">{{ title }}</h4>
			<h4 v-pre class="margin">{{ title }}</h4>
			<div class="flex-center margin">
				<h4 v-text="title" />
				<Buttons
					class="button"
					size="small"
					color="primary"
					@click="title = 'I is another title'"
					>Change title
				</Buttons>
			</div>
			<div v-if="notes.length === 0">No notes, add first note please</div>
			<hr class="container__hr" />
			<ul class="flex-row container__ul">
				<li
					v-for="(item, index) in 15"
					:key="item"
					class="flex-between container__item"
				>
					<strong>{{ index }}:</strong>{{ item }}
				</li>
			</ul>
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
		</div>
	</div>
</template>

<script>
import Buttons from "./Buttons.vue";
export default {
	name: "Components",
	components: {
		Buttons,
	},
	data() {
		//данные, которые есть в нашем приложении
		return {
			placeholderString: "Enter the note",
			title: "List notes",
			inputValue: "",
			notes: ["note 1", "note 2", "note 3"],
			person: {
				firstName: "Eleonora",
				lastName: "Pavlova",
				age: 31,
			},
		};
	},
	computed: {
		doubleCount() {
			console.log("doubleCount");
			return this.notes.length * 2;
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