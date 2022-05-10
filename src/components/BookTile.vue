<template>
  <v-card outlined>
    <v-card-title> {{ book.title }} </v-card-title>
    <v-card-subtitle> by {{ book.author }} </v-card-subtitle>
    <v-card-text>
      <div>{{ book.publishingHouse }}, {{ book.year }}</div>
      {{ book.id }}
    </v-card-text>
    <v-card-actions>
      <v-btn color="deep-purple lighten-2" text @click="borrow">
        Borrow
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: 'BookTile',
  props: ['book'],
  methods: {
    borrow () {
      this.$emit('borrow', this.book.id)
    }
  }
}
</script>
