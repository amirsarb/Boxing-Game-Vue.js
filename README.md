<div>
  <h1 align="center"> Vue.JS - Boxing Game 🧑‍💻</h1>
<h2 style="">Goal:</h2>
  <ul>
  <li>

v-if | v-on | v-model | methods | data | v-for | v-show | v-bind

  </li>
  <li>
  Practicing data / methods / styling
  </li>
    
   </ul>

  <p>
    Screenshot:
  </p>

  <a href="">
    <img
      alt="BoxingGame - Vue.JS"
      src="screenshot.jpg"
    />
  </a>
</div>

<hr />

## Requirements

- Vue 3

## Font

- Jost

## Main Part

`Boxing Game`

# Installation

No need to install any application, just open it via your browser and enjoy it!

# Vue Codes

```javascript
function getRandomValue(min, max) {
  return Math.floor(Math.random() * (max - min)) + min;
}

const app = Vue.createApp({
  data() {
    return {
      playerScore: 100,
      computerScore: 100,
      winner: null,
      moveCounter: 0,
      logGame: [],
    };
  },
  watch: {
    playerScore(value) {
      if (value <= 0 && this.computerScore <= 0) {
        //Draw State
        this.winner = "draw";
      } else if (value <= 0) {
        // Player lost
        this.winner = "computer";
      }
    },
    computerScore(value) {
      if (value <= 0 && this.playerScore <= 0) {
        // A draw
        this.winner = "draw";
      } else if (value <= 0) {
        // Monster lost
        this.winner = "player";
      }
    },
  },
  computed: {
    playerBar() {
      if (this.playerScore < 0) {
        return { width: "0%" };
      }
      return { width: this.playerScore + "%" };
    },
    computerBar() {
      if (this.computerScore < 0) {
        return { width: "0%" };
      }
      return { width: this.computerScore + "%" };
    },

    mySuperMove() {
      return this.moveCounter % 3 !== 0;
    },
  },
  methods: {
    playerFight() {
      this.moveCounter++;
      newVal = getRandomValue(5, 12);
      this.computerScore -= newVal;
      this.computerFight();
      this.addLog("player", "Punch", newVal);
    },
    computerFight() {
      newVal = getRandomValue(8, 16);
      this.playerScore -= newVal;
      this.addLog("computer", "Punch", newVal);
    },
    superMove() {
      this.moveCounter++;
      newVal = getRandomValue(20, 30);
      this.computerScore -= newVal;
      this.computerFight();
      this.addLog("player", "Uppercut", newVal);
    },
    heal() {
      this.moveCounter++;
      newVal = getRandomValue(8, 20);
      if (this.playerScore + newVal > 100) {
        this.playerScore = 100;
      } else {
        this.playerScore += newVal;
      }
      this.computerFight();
      this.addLog("player", "Healed", newVal);
    },
    surrender() {
      this.winner = "computer";
    },
    newGame() {
      this.playerScore = 100;
      this.computerScore = 100;
      this.winner = null;
      this.moveCounter = 0;
      this.logGame = [];
    },
    addLog(person, action, value) {
      this.logGame.unshift({
        actionBy: person,
        actionType: action,
        actionValue: value,
      });
    },
  },
});

app.mount("#game");

```
