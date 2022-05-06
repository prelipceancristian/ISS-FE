<template>
  <!--
  <div class="terminal-container">
    <li v-for="terminal of terminals" :key="terminal.id">
      <TerminalTile :terminal="terminal" />
    </li>
  </div> -->
  <v-container>
    <v-row>
      <v-col v-for="terminal of terminals" :key="terminal.id">
        <TerminalTile :terminal="terminal" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { retrieveTemplates } from '../axios/requests'
import constants from '../common/constants'
import TerminalTile from './TerminalTile'

export default {
  name: 'TerminalScreen',
  components: { TerminalTile },
  data: () => ({
    terminals: []
  }),
  methods: {
    handleRetrieveTerminals () {
      retrieveTemplates().then(response => {
        if (response.status == constants.request_status.success) {
          this.terminals = response.data
        } else {
          console.log(response)
        }
      })
    }
  },
  created () {
    this.handleRetrieveTerminals()
  }
}
</script>

<style>
.terminal-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}
</style>
