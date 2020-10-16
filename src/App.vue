<template>
  <div id="app">

    <div class="Result">
      <section v-if="showResult">
        <ul><li class="attempt goal">
          <div class="Spot" v-for="(color,i) in goal" :style="{color: color}" :key="i" />
        </li></ul>
      </section>
      <button @click.prevent="showResult = !showResult">Show Result</button>
    </div>

    <Form :colors="colors" :goal="goal" @newAttempt="newAttempt" />

    <ul class="Attemps"><li v-for="attempt in attempts" :key="attempt.id" class="attempt">
      <div class="Spot"
        v-for="(color, id) in attempt.colors"
        :style="{color: color}"
        :key="'' + attempt.id + id"
      ></div>
      <div class="Spot smol"
        v-for="(advice,i) in attempt.advices"
        :style="{color: advice}"
        :key="i"
      ></div>
    </li></ul>

  </div>
</template>

<script>
import Form from './components/Form.vue'

export default {
  name: 'App',
  data() {
    return {
      showResult: false,
      goal: [],
      attempts: [],
      colors: ["#67E9DB", "#7C6AB9", "#F070C8", "#F4AC52"],
    }
  },
  methods: {
    rollDice(max = 99) {
      return Math.floor(Math.random()*max);
    },
    newAttempt(currentColors) {
      var currentGoal = [...this.goal];
      const attemptColors = [...currentColors];

      var advices = []
      currentGoal.forEach((cur, i) => {
        if (currentColors.indexOf(cur) === -1) {
          return ;
        } else if (cur === currentColors[i]) {
          advices.push('white');
        } else if (currentColors.indexOf(cur) >= 0) {
          advices.push('black');
        }
        currentGoal[i] = 'nope'
        currentColors[currentColors.indexOf(cur)] = 'nope'
      })

      this.attempts.push({
        id: this.attempts.length,
        colors: attemptColors,
        advices: advices
      })
    }
  },
  components: {
    Form
  },
  created() {
    for (var i = 4; i > 0; i--) {
      this.goal.push(this.colors[this.rollDice(this.colors.length)])
    }
  }
}
</script>

<style lang="scss" src="./assets/stylesheet.scss"></style>
