<template>
  <div class="dialogbox">
    <div class="body">
      <span class="tip tip-left"></span>
      <div class="message">
        <span
          ><li v-for="(review, index) in reviews" :key="index">
            {{ review.name }} : "{{ review.review }}"
          </li></span
        >
      </div>
    </div>
  </div>
  <!-- <div class="review-container">
    <h3>Comment:</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        {{ review.name }}
        "{{ review.review }}"
      </li>
    </ul>
  </div> -->
</template>

<script>
export default {
  props: ['reviews']
}
</script>

<style scoped>
.tip {
  width: 0px;
  height: 0px;
  position: absolute;
  background: transparent;
  border: 10px solid #ccc;
}
.tip-left {
  top: 10px;
  left: -25px;
  border-top-color: transparent;
  border-left-color: transparent;
  border-bottom-color: transparent;
}
.body .message {
  min-height: 30px;
  border-radius: 3px;
  font-family: Arial;
  font-size: 14px;
  line-height: 1.5;
  color: #797979;
}
.dialogbox .body {
  position: relative;
  max-width: 300px;
  height: auto;
  margin: auto;
  padding: 5px;
  background-color: #dadada;
  border-radius: 3px;
  border: 5px solid #ccc;
  margin-bottom: 10px;
}
</style>
