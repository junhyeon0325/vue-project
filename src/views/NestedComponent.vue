<template>
  <div class="parent-container">
    {{ msg }} // {{ age }}
    <button @click="toggleDetailes">Toggle</button>
    <!-- 호출될때마다 is누르면 on 누르면 off -->
    <!-- v-on:click="toggleDetailes"을 축약형으로 쓴거임, v-on: == click -->
    <PageTitle
      v-bind:title="title"
      v-bind:likes="likeCnt"
      v-bind:isOK="OkVal"
      :memberList="members"
      :isShow="showDetail"
      @child-clicked="handleChildClick"
      ref="page-component"
    />
    <!-- 현재 컴포넌트에 PageTitle컴포넌트가 그려진다, 그리고 props를 선언해줘야한다. -->
    <!-- v-bind는 생략 가능 -->
    <!-- ref 는 참조값이라고 부름 -->
    <!-- 사용자가 만든 이벤트 @child-clicked -->
  </div>
</template>

<script>
import PageTitle from "../components/PageTitle.vue";
export default {
  components: {
    PageTitle,
  },
  data() {
    return {
      msg: "Parent Component",
      age: 0,
      title: "Dynamic Data from Parent",
      likeCnt: 3,
      OkVal: true,
      showDetail: true,
      members: [
        { name: "father", age: 40 },
        { name: "mother", age: 35 },
        { name: "son", age: 6 },
      ],
    };
  },
  methods: {
    toggleDetailes() {
      this.showDetail = !this.showDetail; // 누를때마다 boolean타입이 바껴야하니까
    },
    handleChildClick(payload = {}) {
      // {}는 초기값, {}안에 name:'Lee', age:0 을 써도되고 안써도되고
      this.msg = payload.name;
      this.age = payload.age;
    },
  },
  mounted() {
    // console.log(this);
  },
};
</script>

<style scoped>
/*  */
.parent-container {
  border: 2px solid green;
}
</style>
