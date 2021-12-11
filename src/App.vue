<template>
  <div>
    <component :is="Screens[pos]"
               :qustion="UserQuestion"
               :result="UserResult"
               @goto="hGoto"
               @UserQuestion="handleUserQuestion"
               @showResult="ShowResult"
               @startOver="handleStartOver">
    </component>

  </div>
</template>

<script>
import initial from "./components/initial";
import confirm from "./components/confirm";
import result from "./components/result";
import {ref} from "vue";

export default {
  name: 'App',
  components: {
    initial, confirm, result

  },
  setup() {
    let UserQuestion = ref()
    let UserResult = ref()
    let Results = ref(['yes', 'no', 'Maybe', 'sure..try again'])
    let Screens = ['initial', 'confirm', 'result']
    let pos = ref(0)
    let hGoto = (position) => {
      pos.value = position
    }
    let handleUserQuestion = (question) => {
      UserQuestion.value = question

    }
    let getRandomValue = () => {
      return Results.value[Math.floor(Math.random() * Results.value.length)]
    }
    let GenrateResults = () => {
      let rand = getRandomValue();
      if (rand !== ' ') {
        while (rand.value === Results.value) {
          rand = getRandomValue();
        }
      }

      UserResult.value = rand
    }
    let ShowResult = () => {
      GenrateResults()
    }
    let handleStartOver = () => {
      pos.value = 0
      UserResult.value = ' '
      UserQuestion.value = ' '


    }

    return {
      Screens,
      pos,
      hGoto,
      UserQuestion,
      handleUserQuestion,
      UserResult,
      Results,
      ShowResult,
      GenrateResults,
      getRandomValue,
      handleStartOver
    }
  }
}
</script>

<style>
@import "assets/style.css";
</style>
