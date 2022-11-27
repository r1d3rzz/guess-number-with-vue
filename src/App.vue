<template>
  <div id="app" class="text-white text-center mt-5 container-fluid">
    <div class="row">
      <div class="col-md">
        <h1>Guess A Number</h1>
        <h3 class="mb-5">(Between 1 to 20)</h3>
        <div>
          <div class="guessNumber">
            <span>{{ secretNumber }}</span>
          </div>

          <div class="alert alert-warning fs-3" v-if="endGameMessage">
            {{ endGameMessage }}
          </div>
          <hr />
          <div class="row mt-5">
            <div class="col-md-6">
              <div class="card bg-secondary w-50 mx-auto mb-4">
                <div v-if="hint_message">
                  <div class="card-header bg-primary" v-if="is_start">
                    <div>
                      <span>Hint : {{ hint_message }}</span>
                    </div>
                  </div>
                </div>
                <div class="card-body">
                  <input
                    type="number"
                    placeholder="Enter Number"
                    class="form-control"
                    v-if="is_start"
                    v-model="player_number"
                  />
                  <button
                    class="btn btn-dark mt-3"
                    v-if="!is_start"
                    @click="startGame"
                  >
                    Start Game
                  </button>
                  <div v-if="!is_win">
                    <button
                      class="btn btn-dark mt-3"
                      v-if="is_guest"
                      @click="guessNumberBtn"
                    >
                      Guess Number
                    </button>
                  </div>
                  <div v-if="is_restart">
                    <button class="btn btn-warning mt-3" @click="restartBtn">
                      Restart
                    </button>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-md-6">
              <div class="card text-start w-50 mx-auto">
                <div class="card-header bg-secondary">Score Box</div>
                <div class="card-body text-dark">
                  <h5>
                    🧡Live : <b>{{ live }}</b>
                  </h5>
                  <h5 v-if="hightScore">
                    🔥Hight Score : <b>{{ hightScore }}</b>
                  </h5>
                  <h5>
                    ☞Your Score : <b>{{ currentScore }}</b>
                  </h5>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      is_start: false,
      is_win: false,
      is_restart: false,
      is_guest: false,
      guess_number: 0,
      live: 10,
      hightScore: null,
      currentScore: 0,
      endGameMessage: "",
      player_number: "",
      hint_message: "",
      secretNumber: "?",
    };
  },
  methods: {
    startGame() {
      this.hint_message = "";
      this.is_start = true;
      this.is_guest = true;
      this.secretNumber = "?";
      this.guess_number = Math.floor(Math.random() * 20 + 1);
      // console.log(this.guess_number);
    },
    guessNumberBtn() {
      if (this.player_number == "") {
        return (this.hint_message = "Please Enter A Number");
      }

      if (this.player_number > this.guess_number) {
        this.live--;
        this.hint_message = "Larger than a number";
      } else if (this.player_number < this.guess_number) {
        this.live--;
        this.hint_message = "Smaller than a number";
      } else if (this.player_number === this.guess_number) {
        this.secretNumber = this.guess_number;
        this.endGameMessage = "🎉 Congratulations Winner 🎉";
        this.currentScore = this.live;
        this.currentScore > this.hightScore
          ? (this.hightScore = this.currentScore)
          : null;
        this.is_win = true;
        this.is_restart = true;
      }

      if (this.live == 0) {
        this.secretNumber = this.guess_number;
        this.endGameMessage = "😣 Game Over";
        this.is_guest = false;
        this.is_restart = true;
        this.hint_message = "";
        return;
      }
    },
    restartBtn() {
      this.is_win = false;
      this.is_start = false;
      this.is_guest = false;
      this.is_restart = false;
      this.currentScore = 0;
      this.live = 10;
      this.secretNumber = "?";
      this.player_number = "";
      this.endGameMessage = "";
    },
  },
};
</script>

<style>
.guessNumber {
  border: 3px solid white;
  padding: 10px;
  width: 100px;
  margin: 20px auto;
  height: 100px;
  font-size: 50px;
  border-radius: 5px;
}
</style>