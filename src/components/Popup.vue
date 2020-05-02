<template>
  <div class="text-center">
    <v-dialog v-model="popup" width="100%">
      <v-card class="mx-auto" max-width="50%" outlined>
        <v-list-item three-line>
          <v-list-item-content>
            <div
              class="overline mb-4"
              v-for="author in book.volumeInfo.authors"
              :key="author"
            >{{ author }}</div>
            <v-list-item-title class="headline mb-1">{{ book.volumeInfo.title }}</v-list-item-title>
            <v-list-item-subtitle>{{ book.volumeInfo.description }}</v-list-item-subtitle>
          </v-list-item-content>

          <v-list-item-avatar tile size="80" color="grey"></v-list-item-avatar>
        </v-list-item>

        <v-card-actions>
          <v-btn text>Button</v-btn>
          <v-btn text>Button</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    popup: Boolean,
    code: String,
    book: Object
  },
  data() {
    return {};
  }
};
</script>