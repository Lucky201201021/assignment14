<script>
import Square from './components/square.vue'



export default {
  name: "app",
  components: { Square },
  computed: {},
  data() {
    return {
      turnOfX: true,
      reset: false,
      squareValue: Array(9).fill(null),
      status: "",
     
      lines: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ]
    }
  },
  computed: {

  },
  methods: {
    computeStatus() {
  if (this.calculateWinner()) {
    this.status = "Winner: " + this.calculateWinner();
    this.reset = true;
  } else if (this.allSquaresFilled()) {
    this.status = "It's a draw!";
    this.reset = true; 
  } else {
    this.status = (this.turnOfX ? "X" : "O") + "'s turn";
    this.reset = false;
  }
  return this.status;
},

    calculateWinner() {
      for (let i = 0; i < this.lines.length; i++) {
        const [a, b, c] = this.lines[i];
        if (
          this.squareValue[a] && this.squareValue[a] === this.squareValue[b] && this.squareValue[a] === this.squareValue[c]
        ) {
          return this.squareValue[a];
        }
      }
      return null;
    },

    allSquaresFilled() {
  return this.squareValue.every(square => square !== null);
},

    onActionFill(i) {
      if (this.squareValue[i]) {
        return
      }
     
      if (this.turnOfX) {
        this.squareValue[i] = "X"
      } else {
        this.squareValue[i] = "O"
      }
      
      this.setturnOfX()
      return this.squareValue
    },
    setturnOfX() {
      this.turnOfX = !(this.turnOfX);
    },
    newGame() {
      this.squareValue = Array(9).fill(null);
      this.reset = false;
      this.turnOfX = true;
    }
  },

}
</script>

<template>
  <div class="center">
    <h1>Tic Tac Toe</h1>
    <p class="showStatus">{{ computeStatus() }}</p>
    <button class="resetButton" v-if="reset" @click="newGame">Reset</button>
    <div class="row">
      <Square :squareValue="squareValue[0]" @actionFill="onActionFill(0)" />
      <Square :squareValue="squareValue[1]" @actionFill="onActionFill(1)" />
      <Square :squareValue="squareValue[2]" @actionFill="onActionFill(2)" />
    </div>
    <div class="row">
      <Square :squareValue="squareValue[3]" @actionFill="onActionFill(3)" />
      <Square :squareValue="squareValue[4]" @actionFill="onActionFill(4)" />
      <Square :squareValue="squareValue[5]" @actionFill="onActionFill(5)" />
    </div>
    <div class="row">
      <Square :squareValue="squareValue[6]" @actionFill="onActionFill(6)" />
      <Square :squareValue="squareValue[7]" @actionFill="onActionFill(7)" />
      <Square :squareValue="squareValue[8]" @actionFill="onActionFill(8)" />
    </div>
  </div>
</template>


<style scoped>
.center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}



.square {
  width: 80px;
  height: 80px;
  border: 2px solid orange;
  text-align: center;
  font-weight: bold;
  font-size: 32px;
  line-height: 80px;
}

.showStatus {
  color: white;
  background-color: orange;
  border-radius: 5px;
  padding: 6px 10px;
  margin-bottom: 10px;
  font-size: 15px;
  font-weight: bold;
  text-align: center;
}

.resetButton {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  margin-bottom: 10px;
  border-radius: 5px;
  padding: 6px 10px;
  background-color: orange;
  border: none;
  font-size: 20px;
  font-weight: bold;
  color: white;
}

.row {
  display: flex;
  justify-content: center;
}
</style>