<template>
  <v-container>
    <v-row v-if="books.length != 0">
      <v-col v-for="book of books" :key="book.id">
        <BookTile :book="book" @borrow="borrow" />
      </v-col>
    </v-row>
    <div v-else>
      No books found
    </div>
  </v-container>
</template>

<script>
import BookTile from './BookTile'
//import { retrieveBookCopies } from '../axios/requests'
export default {
  name: 'BookList',
  components: { BookTile },
  // data: () => ({
  //   books: []
  // }),
  props: ['books'],
  methods: {
    borrow (bookId) {
      this.$emit('borrow', bookId)
    }
  }
  // created () {
  //   this.handleRetrieveBookCopies()
  // },
  // updated () {
  //   this.handleRetrieveBookCopies()
  // },
  // watch: {
  //   terminalId: function (val) {
  //     console.log(val)
  //   }
  // }
}
</script>
