<template>
  <button type="button" @click="increment">&#9829; {{value}}</button>
</template>

<script>
export default {
  props: ['value'],
  methods: {
    increment() {
      console.log(this.value);
      this.$emit('input', this.value + 1);
    }
  }
}
</script>

<style>
</style>