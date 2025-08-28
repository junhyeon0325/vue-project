<template>
  <h3>Hello, world</h3>
  <p>{{ msg }}</p>
  <p v-text="city"></p>
  <p v-html="htmltext"></p>
  <!-- 실시간으로 적용되는 v-model 이걸 양방향 바인딩 -->
  <input v-model="msg" />
</template>

<script>
export default {
  data() {
    return {
      msg: "안녕하세요",
      city: "서울",
      htmltext: "<b>서울</b>",
    };
  },
};
</script>

<style></style>
