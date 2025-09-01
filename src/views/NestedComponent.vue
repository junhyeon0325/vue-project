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
    <!-- v-bind:title="title"형태를 보면 v-bind는 말그대로 바인딩한다는 의미 {{ 요거 }}, :title=이게 넘어가서 다른 컴포넌트에서 사용하는 변수?임 PageTitle컴포넌트에서 title을 쓰는거 -->
    <!-- "title"이게 지금 현재 컴포넌트에서 export default에 data() {return{여기 안에}}에 값을 초기화 해준거 -->
     <!-- 여기 조금 특이한거 child-clicked 요 부분은 지금 PageTitle.vue에서 값을 $emit을 통해서 값을 받아오는거기 때문에 이 값하고 PageTitle에서 $emit하고 첫값이 여기 child-clicked하고 같아야함 -->
  </div>
</template>

<script>
import PageTitle from "../components/PageTitle.vue"; // 여기서도 PageTitle컴포넌트로 값을 보낼려고 import한 모습

export default {
  components: {
    PageTitle, // PageTitle컴포넌트로 값을 보낼려고
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
