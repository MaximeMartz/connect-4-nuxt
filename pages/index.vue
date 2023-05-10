<template>
  <div>
    <div id="gameboard">
      <div v-for="n in 7" class="column" @click="addPiece($event, n - 1)">
        <div
          v-for="(_cell, index) in startCells[n - 1]"
          class="tile"
          :class="startCells[n - 1][index]"
        ></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data() {
    return {
      startCells: [
        ['', '', '', '', '', ''],
        ['', '', '', '', '', ''],
        ['', '', '', '', '', ''],
        ['', '', '', '', '', ''],
        ['', '', '', '', '', ''],
        ['', '', '', '', '', ''],
        ['', '', '', '', '', ''],
      ],
      turn: 0,
      go: 'red-piece',
      i: 5,
      x: 0,
      y: 0,
    }
  },
  methods: {
    addPiece(e: any, column: any) {
      console.log(this.startCells)
      while (this.i >= 0) {
        if (this.startCells[column][this.i] == '') {
          this.startCells[column][this.i] = this.go
          this.verification()
          this.i = 5
          this.turnCounter()
          break
        } else {
          this.i--
        }
      }
      this.go = this.go === 'red-piece' ? 'yellow-piece' : 'red-piece'
      this.$forceUpdate()
    },

    turnCounter() {
      // make sure there is no softlocking
      this.turn++
      if (this.turn == 42) {
        this.ended('tie')
      }
    },

    verification() {
      // horizontal checks
      for (this.x = 0; this.x <= 3; this.x++) {
        for (this.y = 0; this.y <= 5; this.y++) {
          if (this.startCells[this.x][this.y] != '') {
            if (
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 1][this.y] &&
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 2][this.y] &&
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 3][this.y]
            ) {
              this.ended(this.go)
            }
          }
        }
      }

      // vertical checks
      for (this.x = 0; this.x <= 6; this.x++) {
        for (this.y = 0; this.y <= 2; this.y++) {
          if (this.startCells[this.x][this.y] != '') {
            if (
              this.startCells[this.x][this.y] ==
                this.startCells[this.x][this.y + 1] &&
              this.startCells[this.x][this.y] ==
                this.startCells[this.x][this.y + 2] &&
              this.startCells[this.x][this.y] ==
                this.startCells[this.x][this.y + 3]
            ) {
              this.ended(this.go)
            }
          }
        }
      }

      //diagonal checks

      for (this.x = 0; this.x <= 3; this.x++) {
        for (this.y = 0; this.y <= 2; this.y++) {
          if (this.startCells[this.x][this.y] != '') {
            if (
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 1][this.y + 1] &&
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 2][this.y + 2] &&
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 3][this.y + 3]
            ) {
              this.ended(this.go)
            }
          }
        }
      }

      for (this.x = 0; this.x <= 3; this.x++) {
        for (this.y = 3; this.y <= 5; this.y++) {
          if (this.startCells[this.x][this.y] != '') {
            if (
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 1][this.y - 1] &&
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 2][this.y - 2] &&
              this.startCells[this.x][this.y] ==
                this.startCells[this.x + 3][this.y - 3]
            ) {
              this.ended(this.go)
            }
          }
        }
      }
    }, //verification()

    ended(playing: any) {
      // display winner in an alert
      if (playing == 'red-piece') {
        if (confirm('Le joueur rouge remporte la partie!')) {
          window.location.reload()
        }
      } else if (playing == 'yellow-piece') {
        if (confirm('Le joueur jaune remporte la partie!')) {
          window.location.reload()
        }
      } else {
        if (confirm('This is a draw')) {
          window.location.reload()
        }
      }
    },
  },
})
</script>

<style>
body {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: beige;
  height: 100vh;
}

#gameboard {
  background-color: blue;
  border: solid 15px darkblue;
  padding: 15px;
  display: flex;
  flex-wrap: wrap;
}

.tile {
  width: 100px;
  height: 100px;
  margin: 5px;
  background-color: beige;
  border: solid 5px darkblue;
  border-radius: 50%;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
}

.red-piece {
  background-color: red;
}

.yellow-piece {
  background-color: yellow;
}
</style>
