<template>
  <div class="button button-style">
    <p class="vertical-center">{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: 'InlineButton',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

.button {
    color: #ffffff;
    display: inline-block;
    border-radius: 10px;
    text-align: center;
    font-family: 'Open Sans', sans-serif;
    font-size: 11pt;
    font-weight: bold;
    padding: 0 15px 0 15px;
    height: 35px;
    user-select: none;
    white-space: nowrap;
}

.button-style:hover {
    background-color: #9bd9ff;
}

.button-style {
    background-color: #61b2ec;
}

.button-style:active {
    background-color: #2373ac;
}

.vertical-center {
    margin: 0;
    padding: 7px 0 0 0;
}
</style>
