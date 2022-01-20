<template>
	<v-dialog v-model="dialog" fullscreen transition="dialog-bottom-transition">
		<template v-slot:activator="{ on, attrs }">
			<v-btn
				elevation="2"
				color="primary"
				outlined
				block
				class="mb-10 mt-10"
				dark
				v-bind="attrs"
				v-on="on"
			>
				Сохранить вопросы
			</v-btn>
		</template>
		<v-card>
			<v-toolbar dark color="primary">
				<v-toolbar-items>
					<v-btn dark text @click="clipboard"> Копировать </v-btn>
				</v-toolbar-items>
				<v-spacer></v-spacer>
				<v-btn icon dark @click="dialog = false">
					<v-icon>mdi-close</v-icon>
				</v-btn>
			</v-toolbar>

			<v-divider></v-divider>
			<v-container fluid>
				<v-textarea
					solo
					ref="text"
					:value="questionsAll"
					hide-details="true"
				></v-textarea>
			</v-container>
		</v-card>
	</v-dialog>
</template>

<script>
export default {
	name: "ButtonResulte",

	props: ["questions", "cauntResponsesForFile"],

	data: () => ({
		dialog: false,
	}),

	methods: {
		copyTextArea: function () {
			let all = [];
			for (let i of this.questions) {
				let q = [];
				q = i.responseAll.join(" \n,\n");

				let s = `${i.questions}\n.\n${q}\n.\n${i.correctResponse}\n`;

				all.push(s);
			}

			all.unshift(this.cauntResponsesForFile + "\n");
			all.unshift(this.questions.length + "\n");

			return all.join("");
		},

		clipboard: function () {
			navigator.clipboard.writeText(this.copyTextArea());
			this.$toast("Скопировал");
		},
	},

	computed: {
		questionsAll: function () {
			return this.copyTextArea();
		},
	},
};
</script>

<style>
.v-textarea textarea {
	min-height: 85vh !important;
}
</style>
