<template>
  <div class="container mt-5">
    <h2 v-if="winner">Winner: {{ winner }}</h2>
    <h2 v-else>Players Move: {{ playerTurn }}</h2>
    <button @click="Reset" class="btn btn-success mb-5 mt-2">Reset</button>

    <div v-for="(row, i) in 3" :key="i" class="row1">
      <div v-for="(col, j) in 3" :key="j">
        <button @click="Move(i, j)" class="square">
          {{ squares[i][j] }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Board",
  data() {
    return {
      playerTurn: "X",

      winner: false,

      squares: [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ],

      lines: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ],
    };
  },
  methods: {
    Move(x, y) {
      if (this.winner || this.squares[x][y] !== "") {
        return;
      } else {
        this.squares[x][y] = this.playerTurn;
        this.playerTurn = this.playerTurn === "O" ? "X" : "O";
        this.CheckWinner(this.squares.flat());
        console.log(this.squares.flat());
        console.log(this.winner);
      }
    },

    CheckWinner(array) {
      for (let i = 0; i < this.lines.length; i++) {
        let [a, b, c] = this.lines[i];
        if (
          array[a] != "" &&
          array[b] != "" &&
          array[c] != "" &&
          (array[a] === array[b]) === array[c]
        ) {
          this.winner = true;
        } else {
          this.winner = false;
        }
      }
    },

    Reset() {
      this.playerTurn = "X";
      this.winner = false;
      this.squares = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ];
    },
  },
};
</script>

<style scoped>
.square {
  width: 15vw;
  height: 15vw;
  max-width: 150px;
  max-height: 150px;
  background: #fff;
  text-align: center;
  font-size: 12vw;
  font-weight: bold;
  line-height: 0px;
  border: 1px solid rgb(122, 122, 122);
}
.row1 {
  display: flex;
}
@media screen and (min-width: 1000px) {
  .square {
    font-size: 120px;
  }
}
</style>