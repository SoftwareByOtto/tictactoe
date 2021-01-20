<template>
  <div>
    {{grid}}
    <h1>hello</h1>
    {{turn}}'s turn
    <div class="grid">
      <div class="square" @click="handleClick(0)">{{grid[0]}}</div>
      <div class="square" @click="handleClick(1)">{{grid[1]}}</div>
      <div class="square" @click="handleClick(2)">{{grid[2]}}</div>
      <div class="square" @click="handleClick(3)">{{grid[3]}}</div>
      <div class="square" @click="handleClick(4)">{{grid[4]}}</div>
      <div class="square" @click="handleClick(5)">{{grid[5]}}</div>
      <div class="square" @click="handleClick(6)">{{grid[6]}}</div>
      <div class="square" @click="handleClick(7)">{{grid[7]}}</div>
      <div class="square" @click="handleClick(8)">{{grid[8]}}</div>
    </div>
    <h1>winner</h1>
    the winner is {{winner}} with combo {{winningCombo}}
  </div>
</template>

<script>
export default {
  data() {
    return {
      grid: new Array(9).fill(''),
      turn: 'o',
      totalTurns: 0,
      combos: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4 ,8],
        [2, 4, 6]
      ]
    }
  },
  methods: {
    handleClick(index) {
      // alert('you clicked ' + index)
      if (!this.grid[index].length) {
        this.grid[index] = this.turn
        this.totalTurns++
        this.turn = this.totalTurns < 9 ? (this.turn === 'o' ? 'x' : 'o') : 'draw!'
      }
    }
  },
  computed: {
    winningCombo() {
      return this.combos.map(combo => {
        const [a, b, c] = combo
        const gridA = this.grid[a]
        const gridB = this.grid[b]
        const gridC = this.grid[c]
        return gridA
        if (gridA === 'x' || gridA === 'o') {
          if (gridA === gridB && gridA === gridC) {
            return gridA
          }
        }
      })
    },
    winner() {
      return this.winningCombo !== undefined ? this.grid[this.winningCombo[0]] : 'no winner yet'
    }
  }
}
</script>

<style>
.grid {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
}
.square {
  background-color: gray;
  text-align: center;
  font-size: 52px;
}
.square:nth-child(even) {
  background-color: green;
}
</style>
