<template>
  <section
    :class='classList'
  >
    <slot />
  </section>
</template>

<script>
export default {
  name: 'Surface',
  computed: {
    classList () {
      return [
        'card'
      ]
    }
  }

}
</script>

<style>
  .card {
    display: flex;
    flex-direction: column;
    align-items: center;
    border-radius: 15px;
    background-color: rgb(255, 255, 255);
    padding: 25px;
    text-align: center;
    min-height: 50vh;
    min-width: 50vw;
  }
</style>
