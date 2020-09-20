<template>
  <div class="Form">
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
      color_4: ''
    }
  },
  computed: {
    disableForm() {
      return this.color_1 === '' || this.color_2 === '' || this.color_3 === '' || this.color_4 === ''
    }
  },
  methods: {
    newAttempt() {
      var currentColors = [
        this.color_1,
        this.color_2,
        this.color_3,
        this.color_4,
      ]

      this.$emit('newAttempt', currentColors)
    }
  },
  props: {
    colors: Array,
    goal: Array,
    attempts: Array
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
  bottom: 2.5rem;
  background-color: #fff;

  .Spot:hover + &, &:hover {
    display: block;
  }
}
</style>
