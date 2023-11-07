<template>

<button
  @click="carvePumpkin"
>
  Pick Pumpkin
</button>

<button
 @click="carvePumpkin"
>
Put Pumpkin Back
</button>

<button
 @click="carvePumpkin"
>
Run Carve Pumpkin
</button>

<button
 @click="carvePumpkin"
>
  Pick Winner
</button>

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

</style>
