<template>
  <button
    :class="classList"
    @click="onClick"
  >
    {{ buttonText }}
    <slot />
  </button>
</template>

<script>
export default {
  name: 'QuizButton',
  props: {
    outlined: {
      type: Boolean,
      default: false
    },
    buttonText: {
      type: String,
      default: null
    }
  },
  computed: {
    classList () {
      return [
        'button',
        { 'button--outlined': this.outlined }

      ]
    }
  },
  methods: {
    onClick (event) {
      this.$emit('click', event)
    }
  }

}
</script>

<style>
  .button {
    height: 50px;
    width: 200px;
    border-radius: 25px;
    border: 0 solid #fff;
    background-color: rgba(255, 255, 255, 0.808);
    font-size: 14px;
    font-weight: 700;
    font-family: sans-serif;
    margin: 5px 0;
  }

  .button:active {
    background-color: rgba(83, 30, 119, 0.5);
  }

  .button--outlined {
    border: 3px solid #aaa;
  }

  .button--outlined:active {
    border: 0 solid #fff;
  }

</style>
