<template>
  <div class="header">
    <p class="title">
      {{ msg }}
    </p> 
  </div>
</template>

<script>
import { type } from 'os';
export default {
  name: 'Title',
  props: {
    msg: {
      type: String,
      default: "Title"
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title {
  width: 808px;
  margin: 0 auto;
  border: 1px solid grey;
  background: blue;
  color: white;
  font-size: 30px;
  font-weight: bold;
  font-style: italic;
  margin-top: 20px;
  border-collapse:collapse;
}
</style>
