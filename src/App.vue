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

interface State {
  pickPumpkin(): void,
  putPumpkinBack(): void,
  carvePumpkin(): void,
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
}

type PumpkinContestState = (NoPumpkinState | HasPumpkinState)

class PumpkinContest {
  noPumpkinState: NoPumpkinState
  hasPumpkinState: HasPumpkinState

  pumpkinCount: number
  state: PumpkinContestState

  constructor(count: number) {
    this.noPumpkinState = new NoPumpkinState()
    this.hasPumpkinState = new HasPumpkinState()

    this.pumpkinCount = count
    this.state = new NoPumpkinState()
  }
}

export default {
  setup() {
    const MAX_PUMPKINS: number = 5
    const pumpkinContest:Ref<PumpkinContest> = ref(new PumpkinContest(0))

    const pickPumpkin = (): void => {

    }

    const putPumpkinBack = (): void => {

    }

    const carvePumpkin = (): void => {
      // alert(pumpkinContest.state.carvePumpkin())
      alert('hi')
    }

    const pickWinner = (): void => {

    }

    return {
      MAX_PUMPKINS,
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
