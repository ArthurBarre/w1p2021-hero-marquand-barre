<template>
  <div @click="handleClick()">
  <br>
    <h2>{{expedition}}</h2>
    
  </div>

</template>

<script>
export default {
  props: ['expedition'],
  name: 'expedition',
  methods: {
    handleClick() {
      this.$emit('expedition', this.expedition)
    }
  }
};
</script>
