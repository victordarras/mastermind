<template>
  <div id="app">
    <Form :colors="colors" :goal="goal" />
    <section  v-if="showResult" class="Result">
      <h4>Goal</h4>
      <ul><li class="attempt goal">
        <div class="Spot" v-for="(color,i) in goal" :style="{color: color}" :key="i" />
      </li></ul>
    </section>
    <button @click.prevent="showResult = !showResult">Show Result</button>
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
      colors: ["green", "tomato", "purple", "gold"],
    }
  },
  methods: {
    rollDice(max = 99) {
      return Math.floor(Math.random()*max);
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
