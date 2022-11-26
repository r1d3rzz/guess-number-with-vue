<template>
  <div id="app" class="text-white text-center mt-5 container-fluid">
    <div class="row">
      <div class="col-md">
        <h1>Guess A Number</h1>
        <div>
          <div class="guessNumber">
            <span>?</span>
          </div>
          <hr />
          <div class="row mt-5">
            <div class="col-md-6">
              <div class="card bg-secondary w-50 mx-auto mb-4">
                <div class="card-header bg-primary" v-if="is_start">
                  <div>
                    <span>Hint : Larger Than A Number</span>
                  </div>
                </div>
                <div class="card-body">
                  <input
                    type="number"
                    placeholder="Enter Number"
                    class="form-control"
                    v-if="is_start"
                  />
                  <button
                    class="btn btn-dark mt-3"
                    v-if="!is_start"
                    @click="startGame"
                  >
                    Start Game
                  </button>
                  <button class="btn btn-dark mt-3" v-if="is_start">
                    Guess Number
                  </button>
                </div>
              </div>
            </div>
            <div class="col-md-6">
              <div class="card text-start w-50 mx-auto">
                <div class="card-header bg-secondary">Score Box</div>
                <div class="card-body text-dark">
                  <h5>Live : <b>10</b></h5>
                  <h5>Hight Score : 20</h5>
                  <h5>Your Score : 15</h5>
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
    };
  },
  methods: {
    startGame() {
      this.is_start = true;
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