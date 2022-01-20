<template>
	<v-dialog v-model="dialog" width="500">
		<template v-slot:activator="{ on, attrs }">
			<v-btn
				elevation="2"
				color="primary"
				outlined
				block
				class="mb-10 mt-10"
				v-bind="attrs"
				v-on="on"
			>
				Как пользоваться ?
			</v-btn>
		</template>

		<v-card>
			<v-card-title class="text-h5">
				Тебе реально нужна инструкция ?
			</v-card-title>

			<v-card-text>
				<div>
					<img
						src="http://risovach.ru/upload/2016/02/mem/nedovolnyy-pacan_105185600_orig_.jpg"
						alt="Серьезно что-ли?"
					/>
				</div>
			</v-card-text>

			<v-divider></v-divider>

			<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn color="primary" text @click="dialog = false"> Закрыть </v-btn>
			</v-card-actions>
		</v-card>
	</v-dialog>
</template>

<script>
export default {
	name: "ButtonHowToUse",

	data: () => ({
		dialog: false,
	}),
};
</script>

