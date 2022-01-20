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
        Возьми код
      </v-btn>
    </template>

    <v-card>
      <v-card-text>
        <div>
          <img
            src="https://uploads.hb.cldmail.ru/geekbrains/public/ckeditor_assets/pictures/7056/retina-50aa114f9481829362c57bb2eb959886.jpg"
            alt=""
          />
          <h3>
            Если нужно, вот ссылка на код
            <v-chip
              href="https://github.com/lego5621/Smolensk-State-Medical-University-response-parser"
              link
              small
            >
              GitHub
            </v-chip>
          </h3>
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
  name: "ButtonGetCode",

  data: () => ({
    dialog: false,
  }),
};
</script>

<style>
img {
  width: 100%;
}
</style>
