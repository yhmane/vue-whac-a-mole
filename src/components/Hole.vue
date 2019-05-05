<template>
  <div :class="{'hole': true, mole, land}" @click="caps()"></div>
</template>

<script>
export default {
  name: 'Hole',
  data() {
    return {
      mole: false,
      land: false
    }
  },
  methods: {
    caps() {
      this.$emit('caps');
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hole {
  width: 200px;
  height: 200px;
  border: 1px solid grey;
  float: left;
  border-collapse:collapse;
}
.mole {
   content:url(../images/mole.png);
}
.land {
   content:url(../images/x.png);
}
</style>
