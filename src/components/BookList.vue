<template>
  <v-container>
    <v-row>
      <v-col v-for="book of books" :key="book.id">
        <BookTile :book="book" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import BookTile from './BookTile'
import { retrieveBookCopies } from '../axios/requests'
export default {
  name: 'BookList',
  components: { BookTile },
  data: () => ({
    books: []
  }),
  methods: {
    handleRetrieveBookCopies () {
      retrieveBookCopies('e8da9b1e-e1a3-4d5b-8190-4ff9e2bbc9bd').then(
        response => {
          if (response.data) {
            this.books = response.data
          }
        }
      )
    }
  },
  created () {
    this.handleRetrieveBookCopies()
  }
}
</script>
