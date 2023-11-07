<template>
  <div id="pumpkin-competition-wrapper">
    <div id="title-wrapper">
      <h1>Pumpkin Competition</h1>
    </div>
    <div id="state-display-wrapper">
      <h2>Current State: </h2>
    </div>
    <div id="button-wrapper">
      <div id="eye-1" class="eye"></div>
      <div id="eye-2" class="eye"></div>
      <button
        id="pick-pumpkin"
        class="pumpkin-button"
        @click="pickPumpkin"
        >
        Pick Pumpkin
      </button>

      <button
        id="put-pumpkin-back"
        class="pumpkin-button"
        @click="putPumpkinBack"
        >
        Put Pumpkin Back
      </button>

      <button
        id="carve-pumpkin"
        class="pumpkin-button"
        @click="carvePumpkin"
        >
        Run Carve Pumpkin
      </button>

      <button
        id="pick-winner"
        class="pumpkin-button"
        @click="pickWinner"
        >
          Pick Winner
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { ref, type Ref } from 'vue'

const POSSIBLE_PUMPKIN_DESIGNS = [
  'Ghost', 'Elf', 'Wizard', 'Archer', 'Knight', 'Pikachu', 'Eevee', 'Charmander', 'Scary Face', 'Happy Face', 'Sad Face'
]

class Pumpkin {
  id: string
  design: string

  constructor() {
    this.id = crypto.randomUUID()
    this.design = POSSIBLE_PUMPKIN_DESIGNS[(Math.floor(Math.random() * POSSIBLE_PUMPKIN_DESIGNS.length))]
  }

  toString(): string {
    return 'Pumpkin ID: ' + this.id + ' : with design: ' + this.design 
  }
}

interface State {
  pickPumpkin(): void,
  putPumpkinBack(): void,
  carvePumpkin(): void,
  submitPumpkin(): void,
}

class NoPumpkinState implements State {
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.pumpkinContest = contest
  }

  pickPumpkin = (): void => {
    console.log('You have picked a pumpkin')
    this.pumpkinContest.setState(this.pumpkinContest.getHasPumpkinState())
  }

  putPumpkinBack = (): void => {
    console.log('You do not have a pumpkin to put back!')
  }

  carvePumpkin = (): void => {
    console.log('You do not have a pumpkin to carve!')
  }

  submitPumpkin(): void {
    console.log('You do not have have a pumpkin to submit!')
  }
}

class HasPumpkinState implements State {
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.pumpkinContest = contest
  }

  pickPumpkin = (): void => {
    console.log('You already have a pumpkin')
  }

  putPumpkinBack = (): void => {
    console.log('You put your pumpkin back into the patch')
    this.pumpkinContest.setState(this.pumpkinContest.getNoPumpkinState())
  }

  carvePumpkin = (): void => {
    console.log('You carve your pumpkin!')
    this.pumpkinContest.setState(this.pumpkinContest.getCarvedPumpkinState())
  }

  submitPumpkin(): void {
    console.log('You must have a carved pumpkin for eligible submission!')
  }
}

class CarvedPumpkinState implements State {
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.pumpkinContest = contest
  }

  pickPumpkin = (): void => {
    console.log('You already have a pumpkin carved!')
  }

  putPumpkinBack = (): void => {
    console.log('You would not want to put your already carved pumpkin back!')
  }

  carvePumpkin = (): void => {
    console.log('You already carved your pumpkin!')
  }

  submitPumpkin(): void {
    this.pumpkinContest.addPumpkin(new Pumpkin())
    console.log('You successfullly submit your pumpkin')
    this.pumpkinContest.clearPumpkins()
    this.pumpkinContest.setState(this.pumpkinContest.getNoPumpkinState())
  }
}

type PumpkinContestState = (NoPumpkinState | HasPumpkinState | CarvedPumpkinState)

class PumpkinContest {
  MAX_PUMPKINS: number
  pumpkins: Array<Pumpkin>
  noPumpkinState: NoPumpkinState
  hasPumpkinState: HasPumpkinState
  carvedPumpkinState: CarvedPumpkinState
  state: PumpkinContestState

  constructor() {
    this.MAX_PUMPKINS = 5
    this.pumpkins = []
    this.noPumpkinState = new NoPumpkinState(this)
    this.hasPumpkinState = new HasPumpkinState(this)
    this.carvedPumpkinState = new CarvedPumpkinState(this)
    this.state = new NoPumpkinState(this)
  }

  getNoPumpkinState = (): PumpkinContestState => {
    return this.noPumpkinState
  }

  getHasPumpkinState = (): PumpkinContestState => {
    return this.hasPumpkinState
  }

  getCarvedPumpkinState = (): PumpkinContestState => {
    return this.carvedPumpkinState
  }

  setState = (newState: PumpkinContestState): void => {
    this.state = newState
  }

  pickPumpkin = (): void => {
    this.state.pickPumpkin()
  }

  putPumpkinBack = (): void => {
    this.state.putPumpkinBack()
  }

  carvePumpkin = (): void => {
    this.state.carvePumpkin()
  }

  submitPumpkin(): void {
    this.state.submitPumpkin()
  }

  addPumpkin(pumpkin: Pumpkin): void {
    this.pumpkins.push(pumpkin)
  }

  clearPumpkins(): void {
    this.pumpkins = []
  }

  pickWinner() : void {
    if (this.pumpkins.length >= this.MAX_PUMPKINS) {
      const winner: Pumpkin = this.pumpkins[(Math.floor(Math.random() * this.pumpkins.length))]
      this.pumpkins = []
      alert('Winner is: ' + winner.toString())
    } else {
      alert('Not enough pumpkins have been submitted!')
    }
  }
}

export default {
  setup() {
    const pumpkinContest:Ref<PumpkinContest> = ref(new PumpkinContest())

    const pickPumpkin = (): void => {
      pumpkinContest.value.pickPumpkin()
    }

    const putPumpkinBack = (): void => {
      pumpkinContest.value.putPumpkinBack()
    }

    const carvePumpkin = (): void => {
      pumpkinContest.value.carvePumpkin()
    }

    const submitPumpkin = (): void => {
      pumpkinContest.value.submitPumpkin()
    }

    const pickWinner = (): void => {
      pumpkinContest.value.pickWinner()
    }

    return {
      pickPumpkin,
      putPumpkinBack,
      pumpkinContest,
      carvePumpkin,
      submitPumpkin,
      pickWinner,
    }
  }
}

</script>

<style scoped>
  #pumpkin-competition-wrapper{
    border: 2px solid orange;
    display: flex;
    height: 100vh;
    width: 100%;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    padding: 0;

    position: relative;
    width: 100%;
    height: 100vh;
    background-color: #4a4a4a; /* Dark background */
    overflow: hidden;
  }

  @keyframes blink {
    0%{
      opacity: 0;
    }
    95% {
      opacity: 0;
    }
    100% {
      opacity: 50%;
    }
  }

  .eye {
    position: absolute;
    width: 20px;
    height: 50px;
    background-color: rgba(255, 255, 255, 0.129);
    border-radius: 100%;
    margin: auto;
  }

  #eye-1 {
    left: 25%;
    top: 5%;
    animation: blink 15s infinite;
  }

  #eye-2 {
    left: 75%;
    top: 15%;
    animation: blink 15s infinite;
  }

  .eye::before {
    content: '';
    position: absolute;
    top: 10px;
    left: 5px;
    width: 10px;
    height: 30px;
    background-color: #000;
    border-radius: 50%;
  }

  .pumpkin-button {
    height: 4em;
    margin: .2em;
    background-color: #e67e22; /* Pumpkin orange */
    border: 2px solid #544e4e; /* Dark border for contrast */
    color: #fff; /* White text for readability */
    font-weight: bold;
    border-radius: 4em; /* Rounded corners */
    cursor: pointer;
    transition: all 0.3s ease; /* Smooth transition for button press effect */
  }

  .pumpkin-button:hover {
    background-color: #d35400; /* A darker orange on hover */
  }

  .pumpkin-button:active {
    box-shadow: 0 1px #666; /* Less shadow to simulate button press */
    transform: translateY(3px); /* Move the button down to simulate press */
  }

  /* Optional: A stem-like element for the button */
  .pumpkin-button::before {
    content: "";
    display: block;
    position: absolute;
    top: -16px;
    left: 50%;
    transform: translateX(-50%);
    width: 6px;
    height: 16px;
    background-color: #27ae60; /* Color of the stem */
    border-radius: 50%;
  }

</style>
