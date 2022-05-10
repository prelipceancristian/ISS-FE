<template>
  <v-card class="mx-auto mt-10" max-width="300" raised rounded>
    <v-img height="250" src="../assets/library.jpg"></v-img>

    <v-card-title>{{ terminal.name }}</v-card-title>

    <v-card-text>
      <div>
        {{ terminal.address }}
      </div>
    </v-card-text>

    <v-divider class="mx-4"></v-divider>

    <v-card-title>Time table</v-card-title>
    <v-card-text>
      <div>
        {{ timetable1 }}
      </div>
      <div>
        {{ timetable2 }}
      </div>
      <div>
        {{ timetable3 }}
      </div>
    </v-card-text>
    <v-card-title>Book copies available: {{ getBookCopyCount() }}</v-card-title>
    <v-card-actions>
      <v-btn color="deep-purple lighten-2" text @click="selectTerminal">
        Check books
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: ['terminal'],
  name: 'TerminalTile',
  data: () => ({
    timetable1: 'Mon-Fri: 09:00 - 17:00',
    timetable2: 'Sat: 09:00 - 13:00',
    timetable3: 'Sun: Closed'
  }),
  methods: {
    selectTerminal () {
      this.$emit('selectTerminal', this.terminal.id)
    },
    getBookCopyCount () {
      return this.terminal.bookCopies.length
    }
  },
  computed: {}
}
</script>
