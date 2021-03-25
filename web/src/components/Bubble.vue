<template>
  <div class="bubble">
    <h4 class="text bubble-from">Sample bot</h4>
    <div class="text" v-html="msg" />
  </div>
</template>

<script>
export default {
  name: 'Bubble',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

.bubble {
    background-color: #ffffff;
    color: #000000;
    display: block;
    padding: 8px 26px 8px 13px;
    border-radius: 10px;
    max-width: 430px;
    min-width: 100px;
    border: 1px solid #eeeeee;
    white-space: pre-line;
}
.text {
    font-family: 'Open Sans', sans-serif;
    font-size: 11pt;
    margin-top: 0px;
    margin-bottom: 0px;
    text-align: left;
}
.bubble-from {
    font-weight: bold;
    color: #168acd;
}
</style>
