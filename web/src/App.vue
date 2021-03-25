<template>
  <div id="app">
    <div id="bubble-container">
      <div v-for="(msg, index) in state.messages" :key="index">
          <div class="full-message">
            <Bubble :msg="msg.text" />
            <div
              v-for="(row, index) in msg.rows"
              :key="index"
              class="row-container"
            >
              <div v-if="showControlButtons" class="row-actions">
                <button @click="addButtonToRow(row)">Add button</button>
                <button @click="removeRow(msg.rows, index)">Remove row</button>
              </div>
              <div class="buttons-row">
                <InlineButton 
                  v-for="(btn, index) in row"
                  :key="index"
                  :msg="btn.text"
                  @click="jumpState(btn.state)"
                  class="button"
                />
              </div>
            </div>
          </div>
          <br>
          <button v-if="showControlButtons" @click="addRow(msg.rows)">Add row</button>
      </div>
    </div>
    <div id="control-menu">
      <h1>Control Menu</h1>

      <span>Current state: {{ selected }}</span>

      <select v-model="currentState">
        <option v-for="(obj, state) in states" :key="state" :value="state">
          {{ state }}
        </option>
      </select>
      <br>
      <input type="checkbox" v-model="showControlButtons" />
      <label for="checkbox">Show control buttons</label>
      <br>
      <br>


      JSON content:
      <br>
      <textarea class="json-project" v-model="jsonProject"></textarea>
    </div>
  </div>
</template>

<script>
import Bubble from './components/Bubble.vue'
import InlineButton from './components/InlineButton.vue'

export default {
  data() {
    return {
      states: {
        "state1": {
          messages: [
            {
              text: "This is state 1.\n\nEnjoy.",
              rows: [
                [{text: "🤝 Jump to state 2", state: "state2"}, {text: "Useless button"}]
              ]
            }
          ]
        },
        "state2": {
          messages: [
            {
              text: "This is another state.",
              rows: [
                [{text: "Go back", state: "state1"}, {text: "Yet another button"}]
              ]
            }
          ]
        }
      },
      currentState: "state1",
      showControlButtons: false
    }
  },
  name: 'App',
  components: {
    Bubble,
    InlineButton
  },
  computed: {
    state() {
      return this.states[this.currentState]
    },
    jsonProject: {
      get() {
        return JSON.stringify(this.states)
      },
      set(newJSON) {
        try {
          const newStates = JSON.parse(newJSON)
          console.log(newStates)
          this.states = newStates
        } catch (e) {
          console.log('invalid json')
        }
      }
    }
  },
  methods: {
    jumpState(newState) {
      if (!(newState in this.states)) {
        console.log('state ', newState, ' is not found')
        return
      }
      this.currentState = newState
    },
    addButtonToRow(row) {
      row.push({
        text: "New button"
      })
    },
    addRow(rows) {
      rows.push([])
    },
    removeRow(rows, index) {
      rows.splice(index, 1)
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #f5f5f5;
  margin: 0;
  padding: 0;
  padding-top: 60px;
  padding-left: 100px;
  min-height: 1500px;
}
#bubble-container {
  width: 900px;
  float: left;
}
#control-menu {
  background-color:#ffffff;
  width: 500px;
  display: inline-block;
  padding: 0 20px 20px 20px;
}
.json-project {
  width: 100%;
  min-height: 100px;
}
.buttons-row {
  display: flex;
  padding-top: 3px;
}
.full-message {
  display: inline-block;
  padding-top: 10px;
}
.row-container{
  display: block;
  overflow: visible;
  position: relative;
}
.button {
  flex-basis: 0;
  flex-grow: 1;
}
.row-actions {
  position: absolute;
  right: -190px;
  top: 10px;
}
</style>
