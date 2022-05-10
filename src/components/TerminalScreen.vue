<template>
  <v-container>
    <v-row>
      <v-col v-for="terminal of terminals" :key="terminal.id">
        <TerminalTile :terminal="terminal" @selectTerminal="selectTerminal" />
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
    },
    selectTerminal (payload) {
      this.$emit('selectTerminal', payload)
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
