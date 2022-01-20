<template>
	<v-app>
		<v-container>
			<v-row>
				<v-col cols="12" sm="9" class="mb-10 mt-10">
					<v-text-field
						label="Вопрос"
						outlined
						clearable
						hide-details="true"
						v-model="questions"
					></v-text-field>
					<ol>
						<li class="mt-4">
							<v-text-field clearable v-model="responseOne"></v-text-field>
						</li>
						<li class="mt-4">
							<v-text-field clearable v-model="responseTwo"></v-text-field>
						</li>
						<li class="mt-4">
							<v-text-field clearable v-model="responseThee"></v-text-field>
						</li>
						<li class="mt-4">
							<v-text-field clearable v-model="responseFour"></v-text-field>
						</li>
						<li class="mt-4">
							<v-text-field clearable v-model="responseFive"></v-text-field>
						</li>
						<li class="mt-4">
							<v-text-field clearable v-model="responseSix"></v-text-field>
						</li>
					</ol>

					<v-row>
						<v-col cols="12" sm="2" class="mb-10 mt-10">
							<v-text-field
								label="Ответ"
								outlined
								clearable
								hide-details="true"
								v-model="correctResponse"
								@keypress="NumbersOnlyResponse"
							></v-text-field>
						</v-col>
					</v-row>

					<v-btn elevation="2" color="primary" class="mt-5" @click="add">
						Добавить вопрос
					</v-btn>
				</v-col>

				<v-col cols="12" class="mb-10" sm="3">
					<ButtonResulte :questions="readyResponse" :cauntResponsesForFile="cauntResponsesForFile" />
					<ButtonHowToUse />
					<ButtonGetCode />

					<v-text-field
						label="Всего вопросов"
						outlined
						hide-details="true"
						:value="readyResponse.length"
						readonly
						class="mb-10"
					></v-text-field>

					<v-text-field
						label="Вопросов из файла использовать"
						outlined
						hide-details="true"
						v-model="cauntResponsesForFile"
						@keypress="NumbersOnly"
					></v-text-field>
				</v-col>

				<v-col cols="12" class="mt-15" v-if="readyResponse.length">
					<h1>Готовые вопросы</h1>
				</v-col>

				<v-col
					cols="12"
					sm="9"
					class="mt-10"
					v-for="i in readyResponse"
					:key="i.questions + Math.random()"
				>
					<v-sheet color="grey darken-4 rounded-xl" elevation="11" class="pa-5">
						<v-text-field
							label="Вопрос"
							outlined
							hide-details="true"
							readonly
							:value="i.questions"
						></v-text-field>
						<ol>
							<li
								v-for="o in i.responseAll"
								:key="Math.random() + o"
								class="mt-4readyResponse.length"
							>
								<v-text-field :value="o" readonly></v-text-field>
							</li>
						</ol>

						<v-row>
							<v-col cols="12" sm="2" class="mb-10 mt-10">
								<v-text-field
									label="Ответ"
									outlined
									hide-details="true"
									v-model="i.correctResponse"
									readonly
								></v-text-field>
							</v-col>
						</v-row>

						<v-btn elevation="2" color="error" @click="remove(i)">
							Удалить вопрос
						</v-btn>
					</v-sheet>
				</v-col>
			</v-row>
		</v-container>
	</v-app>
</template>

<script>

export default {
	name: "App",


	data: () => ({
		cauntResponsesForFile: 1,

		questions: "",

		responseOne: "",
		responseTwo: "",
		responseThee: "",
		responseFour: "",
		responseFive: "",
		responseSix: "",

		correctResponse: "",

		readyResponse: [],
	}),

	methods: {

		NumbersOnly(evt) {
			evt = evt ? evt : window.event;
			var charCode = evt.which ? evt.which : evt.keyCode;
			if (
				charCode > 31 &&
				(charCode < 48 || charCode > 57) &&
				charCode !== 46
			) {
				evt.preventDefault();
			} else {
				return true;
			}
		},

		NumbersOnlyResponse(evt) {
			if (this.correctResponse.length >= 1) {
				evt.preventDefault();
			} else {
				return this.NumbersOnly(evt);
			}
		},

		add: function () {
			if (this.questions == "") {
				this.$toast("Введи вопрос");
				return;
			}

			if (this.correctResponse == "") {
				this.$toast("Укажи правильный ответ");
				return;
			}

			this.readyResponse.unshift({
				questions: this.questions,
				responseAll: [
					this.responseOne,
					this.responseTwo,
					this.responseThee,
					this.responseFour,
					this.responseFive,
					this.responseSix,
				],
				correctResponse: this.correctResponse,
			});

			this.responseOne = "";
			this.responseTwo = "";
			this.responseThee = "";
			this.responseFour = "";
			this.responseFive = "";
			this.responseSix = "";

			this.questions = "";
			this.correctResponse = "";
			this.$toast("Добавил");
		},

		remove: function (el) {
			let index = this.readyResponse.indexOf(el);
			this.readyResponse.splice(index, 1);
			this.$toast("Удалил");
		},
	},
};
</script>