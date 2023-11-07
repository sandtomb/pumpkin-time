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
import { ref } from 'vue'

export default {
  setup() {
    const MAX_PUMPKINS: number = 5

    const pumpkinContest = ref({})

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
