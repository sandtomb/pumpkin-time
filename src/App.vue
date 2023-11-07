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
  constructor() { }
  pickPumpkin = (): void => {
    console.log('You have picked a pumpkin')
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
  constructor() { }
  pickPumpkin = (): void => {
    console.log('You already have a pumpkin')
  }
  putPumpkinBack = (): void => {
    console.log('You put your pumpkin back into the patch')
  }
  carvePumpkin = (): void => {
    console.log('You carve your pumpkin!')
  }
  submitPumpkin(): void {
    console.log('You must have a carved pumpkin for eligible submission!')
  }
}

class CarvedPumpkinState implements State {
  constructor() { }
  pickPumpkin = (): void => {
    console.log('You already have a pumpkin')
  }
  putPumpkinBack = (): void => {
    console.log('You put your pumpkin back into the patch')
  }
  carvePumpkin = (): void => {
    console.log('You carve your pumpkin!')
  }
  submitPumpkin(): void {
    console.log('You successfullly submit your pumpkin')
  }
}

type PumpkinContestState = (NoPumpkinState | HasPumpkinState | CarvedPumpkinState)

class PumpkinContest {
  MAX_PUMPKINS: number

  noPumpkinState: NoPumpkinState
  hasPumpkinState: HasPumpkinState
  carvedPumpkinState: CarvedPumpkinState

  pumpkins: Array<Pumpkin>
  state: PumpkinContestState

  constructor() {
    this.MAX_PUMPKINS = 5
    this.noPumpkinState = new NoPumpkinState()
    this.hasPumpkinState = new HasPumpkinState()
    this.carvedPumpkinState = new CarvedPumpkinState()

    this.pumpkins = []
    this.state = new NoPumpkinState()
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

    }

    const putPumpkinBack = (): void => {

    }

    const carvePumpkin = (): void => {
      // alert(pumpkinContest.state.carvePumpkin())
      alert('hi')
    }

    const pickWinner = (): void => {
      return pumpkinContest.value.pickWinner()
    }

    return {
      pickPumpkin,
      putPumpkinBack,
      pumpkinContest,
      carvePumpkin,
      pickWinner,
    }
  }
}
  
</script>

<style scoped>

</style>
