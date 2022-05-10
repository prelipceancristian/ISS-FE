<template>
  <v-app style="background-color: rgba(46,64,87);">
    <v-app-bar app dark :color="constants.mainBlue">
      <v-btn icon @click="isNavigationOpen = !isNavigationOpen">
        <v-icon>mdi-menu</v-icon>
      </v-btn>
      <h1>Library-online</h1>
      <v-spacer></v-spacer>
      <User :user="testUser" v-if="isUserLoggedIn"></User>
    </v-app-bar>
    <v-navigation-drawer
      app
      v-model="isNavigationOpen"
      width="300"
      dark
      temporary
      :color="constants.black"
      v-if="isUserLoggedIn && isNavigationOpen"
    >
      <NavigationDrawerContent />
    </v-navigation-drawer>
    <v-main>
      <!--<Tiles v-if="isUserLoggedIn" />-->
      <TerminalScreen
        v-if="isUserLoggedIn && isTerminalListDisplayed"
        @selectTerminal="handleSelectTerminal"
      />
      <LoginScreen v-if="!isUserLoggedIn" @login="handleLogin" />
      <BookList
        v-if="isUserLoggedIn && isBookListDisplayed"
        :books="books"
        @borrow="handleBorrow"
      />
    </v-main>
  </v-app>
</template>

<script>
//import Tiles from './components/Tiles'
import LoginScreen from './components/LoginScreen'
import constants from './common/constants'
import User from './components/User'
import NavigationDrawerContent from './components/NavigationDrawerContent'
import TerminalScreen from './components/TerminalScreen'
import BookList from './components/BookList'
import { retrieveBookCopies } from './axios/requests.js'
import { borrowBook } from './axios/requests.js'

export default {
  name: 'App',

  components: {
    //Tiles,
    User,
    NavigationDrawerContent,
    LoginScreen,
    TerminalScreen,
    BookList
  },

  data: () => ({
    isNavigationOpen: false,
    constants: constants,
    testUser: {
      imageURL: '',
      name: '',
      username: '',
      id: ''
    },
    isUserLoggedIn: false,
    isTerminalListDisplayed: false,
    isBookListDisplayed: false,
    terminalId: '',
    books: []
  }),

  methods: {
    handleLogin (payload) {
      let user = payload.user
      this.testUser.name = user.name
      this.testUser.username = user.username
      this.testUser.id = user.id
      this.isUserLoggedIn = true
      this.isTerminalListDisplayed = true
    },
    handleSelectTerminal (terminalId) {
      retrieveBookCopies(terminalId).then(response => {
        if (response.status == '200') {
          this.books = response.data
          console.log(response.data)
          this.isTerminalListDisplayed = false
          this.isBookListDisplayed = true
        } else {
          console.log(response.data)
        }
      })
    },
    handleBorrow (bookId) {
      var payload = {
        bookCopyId: bookId,
        userId: this.testUser.id,
        deadline: '2022-07-07'
      }
      console.log(payload)
      borrowBook(payload).then(response => {
        if (response.status == '200') {
          this.books = this.books.filter(function (value) {
            return value.id != bookId
          })
        } else {
          console.log(response.data)
        }
      })
    }
  }
}
</script>
