<template>
  <v-card outlined>
    <v-card-title> {{ book.title }} </v-card-title>
    <v-card-subtitle> by {{ book.author }} </v-card-subtitle>
    <v-card-text> {{ book.publishingHouse }}, {{ book.year }} </v-card-text>
    <v-card-actions>
      <v-btn color="deep-purple lighten-2" text @click="reserve">
        Reserve
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: 'BookTile',
  props: ['book']
}
</script>
