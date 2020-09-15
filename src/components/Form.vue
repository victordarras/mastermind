<template>
  <div class="hello">
    <form @submit.prevent="newAttempt()">
      <section>
        <div class="Spot" :style="{color: color_1}"></div>
        <div class="spot-selector">
          <input class="Spot" v-for="color in colors" :key="color" type="radio" v-model="color_1" name="value-1" :value="color" :style="{color: color}" />
        </div>
      </section>
      <section>
        <div class="Spot" :style="{color: color_2}"></div>
        <div class="spot-selector">
          <input class="Spot" v-for="color in colors" :key="color" type="radio" v-model="color_2" name="value-2" :value="color" :style="{color: color}" />
        </div>
      </section>
      <section>
        <div class="Spot" :style="{color: color_3}"></div>
        <div class="spot-selector">
          <input class="Spot" v-for="color in colors" :key="color" type="radio" v-model="color_3" name="value-3" :value="color" :style="{color: color}" />
        </div>
      </section>
      <section>
        <div class="Spot" :style="{color: color_4}"></div>
        <div class="spot-selector">
          <input class="Spot" v-for="color in colors" :key="color" type="radio" v-model="color_4" name="value-4" :value="color" :style="{color: color}" />
        </div>
      </section>
      <button type="submit" :disabled="disableForm">New Try </button>
    </form>
    <hr>
    <h4 v-if="attempts.length">Rounds ({{attempts.length}})</h4>
    <ul><li v-for="attempt in attempts" :key="attempt.id" class="attempt">
      <div class="Spot"
        v-for="(color,id) in attempt.colors"
        :style="{color: color}"
        :key="attempt.id + id + color"
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
export default {
  name: 'Form',
  data() {
    return {
      color_1: '',
      color_2: '',
      color_3: '',
      color_4: '',
      attempts: []
    }
  },
  computed: {
    disableForm() {
      return this.color_1 === '' || this.color_2 === '' || this.color_3 === '' || this.color_4 === ''
    }
  },
  methods: {
    newAttempt() {
      var currentGoal = [...this.goal];
      // var result = []
      var currentColors = [
        this.color_1,
        this.color_2,
        this.color_3,
        this.color_4,
      ]

      var advices = []
      currentGoal.forEach((cur, i) => {
        if (currentColors.indexOf(cur) === -1) {
          return console.log('nope' + 1, currentColors )
        } else if (cur === currentColors[i]) {
          console.log('nice')
          advices.push('white');
        } else if (currentColors.indexOf(cur) >= 0) {
          console.log('ok', currentColors)
          advices.push('black');
        }
        currentGoal[i] = 'nope'
        currentColors[currentColors.indexOf(cur)] = 'nope'
      })

      this.attempts.push({
        id: this.attempts.length,
        colors: [
          this.color_1,
          this.color_2,
          this.color_3,
          this.color_4,
        ],
        advices: advices
      })
    }
  },
  props: {
    colors: Array,
    goal: Array
  }
}
</script>

<style scoped lang="scss">
section {
  position: relative;
}
.spot-selector {
  display: none;
  position: absolute;
  top: 2.5rem;
  background-color: #fff;

  .Spot:hover + &, &:hover {
    display: block;
  }
}
</style>
