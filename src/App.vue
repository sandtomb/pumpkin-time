<template>
  <div id="pumpkin-competition-wrapper">
    <div id="title-wrapper">
      <h1>Pumpkin Carving Competition</h1>
    </div>
    <div>
      <h2>
        Current Pumpkin Count:
        {{ pumpkinContest.pumpkins.length }} / {{ pumpkinContest.MAX_PUMPKINS }}
      </h2>
    </div>
    <div id="state-display-wrapper">
      <div>
        <h4>
          Current State: 
        </h4>
      </div>
      <div id="current-state">
        {{ stateName }}
      </div>
    </div>
    <div id="button-wrapper">
      <div id="eye-1" class="eye"></div>
      <div id="eye-2" class="eye"></div>
      <div id="eye-3" class="eye"></div>
      <div id="eye-4" class="eye"></div>
      <div id="eye-5" class="eye"></div>
      <div id="eye-6" class="eye"></div>
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
        id="submit-pumpkin"
        class="pumpkin-button"
        @click="submitPumpkin"
        >
          Submit Pumpkin
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
import {
  ref,
  type Ref,
} from 'vue'

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
  name: string,
  pickPumpkin(): void,
  putPumpkinBack(): void,
  carvePumpkin(): void,
  submitPumpkin(): void,
}

class NoPumpkinState implements State {
  name: string
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.name = 'No Pumpkin'
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
  name: string
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.name = 'Has Pumpkin'
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
    console.log('You must have a carved pumpkin for an eligible submission!')
  }
}

class CarvedPumpkinState implements State {
  name: string
  pumpkinContest: PumpkinContest

  constructor(contest: PumpkinContest) {
    this.name = 'Has Carved Pumpkin'
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
    const pumpkin: Pumpkin = new Pumpkin()
    this.pumpkinContest.addPumpkin(pumpkin)
    alert('You have successfully submitted your pumpkin: ' + pumpkin.toString())
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
    this.state = this.noPumpkinState
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
    if (this.isFull()) {
      alert('Carving Competition is full - Time to select a winner!')
    } else {
      this.state.submitPumpkin()
    }
  }

  addPumpkin(pumpkin: Pumpkin): void {
    this.pumpkins.push(pumpkin)
  }

  clearPumpkins(): void {
    this.pumpkins = []
  }

  isFull(): boolean {
    return this.pumpkins.length >= this.MAX_PUMPKINS
  }

  pickWinner() : void {
    if (this.pumpkins.length >= this.MAX_PUMPKINS) {
      const winner: Pumpkin = this.pumpkins[(Math.floor(Math.random() * this.pumpkins.length))]
      this.pumpkins = []
      this.setState(this.getNoPumpkinState())
      alert('Winner is: ' + winner.toString())
    } else {
      alert('Not enough pumpkins have been submitted!')
    }
  }
}

export default {
  setup() {
    const pumpkinContest:Ref<PumpkinContest> = ref(new PumpkinContest())
    const stateName: Ref<string> = ref(pumpkinContest.value.state.name)

    const pickPumpkin = (): void => {
      pumpkinContest.value.pickPumpkin()
      stateName.value = pumpkinContest.value.state.name
    }

    const putPumpkinBack = (): void => {
      pumpkinContest.value.putPumpkinBack()
      stateName.value = pumpkinContest.value.state.name
    }

    const carvePumpkin = (): void => {
      pumpkinContest.value.carvePumpkin()
      stateName.value = pumpkinContest.value.state.name
    }

    const submitPumpkin = (): void => {
      pumpkinContest.value.submitPumpkin()
      stateName.value = pumpkinContest.value.state.name
    }

    const pickWinner = (): void => {
      pumpkinContest.value.pickWinner()
      stateName.value = pumpkinContest.value.state.name
    }

    return {
      pumpkinContest,
      stateName,
      pickPumpkin,
      putPumpkinBack,
      carvePumpkin,
      submitPumpkin,
      pickWinner,
    }
  }
}

</script>

<style scoped>
  #pumpkin-competition-wrapper{
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

  #eye-3 {
    left: 25%;
    top: 15%;
    opacity: 20%;
    animation: blink 5s infinite;
  }

  #eye-4 {
    left: 15%;
    top: 85%;
    opacity: 20%;
    animation: blink 14s infinite;
  }

  #eye-5 {
    left: 15%;
    top: 7%;
    opacity: 20%;
    animation: blink 8s infinite;
  }

  #eye-6 {
    left: 75%;
    top: 85%;
    opacity: 20%;
    animation: blink 7s infinite;
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

  #state-display-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
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

  #button-wrapper {
    display: flex;
    justify-content: center;
  }

  #title-wrapper {
    display: flex;
    justify-content: center;
  }

  #current-state {
    position: relative;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    min-width: 4em;
    text-align: center;
    height: 2em;
    padding: .4em;
    border: .2em solid transparent; /* Make border transparent initially */
    border-radius: 2em;
    margin-left: .2em;
    overflow: hidden; /* Ensure the pseudo-element does not extend outside */
  }

  @keyframes trace-border {
  0% {
    box-shadow: inset 0 0 0 0 #d35400;
  }
  80% {
    box-shadow: inset 0 0 0 .1em #d35400;
  }
  100% {
    box-shadow: inset 0 0 0 .2em #d35400;
  }
}

#current-state::before {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  border-radius: inherit; /* Use the same border-radius as the parent */
  animation: trace-border 5s infinite; /* Adjust the timing as needed */
}

</style>
