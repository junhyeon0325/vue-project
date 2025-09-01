<template>
  <div class="child-container">
    {{ msg }}
    <h3>{{ title }}</h3>

    <div v-if="isShow">
      <!-- 보였다가 안보였다가 해볼려고 -->
      <p>Likes: {{ likes }}</p>
      <p>is OK ? {{ isOK ? "Yes" : "No" }}</p>
    </div>

    <!-- 안에 조건식을 쓸 수 있음 -->

    <h3>Member List</h3>
    <ul>
      <li v-for="(family, i) in memberList" :key="i">
        {{ family.name }} - {{ family.age }} year old.
      </li>
    </ul>

    <input v-model="name" />
    <input type="text" v-model="age" />
    <button @click="callParentEvent">call parent event</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "Child component",
      name: "",
      age: 0,
    };
  },
  props: {
    title: { type: String, default: "Default Title" }, // 문자열
    likes: { type: Number, default: 0 }, // 숫자
    isOK: { type: Boolean, default: false }, // 불리언타입
    isShow: { type: Boolean, default: true },
    memberList: {
      type: Array,
      default: () => [],
    }, // Object, 배열은 초기값을 함수로 만들어야함, return은 생략가능
  },
  methods: {
    // 컴포넌트 내에서 사용할 메소드 정의
    callParentEvent() {
      // this.$emit("child-clicked", "자식 컴포넌트에서 호출함."); // 부모 컴포넌트로 이벤트 송출하겠다 라는 의미
      // 첫번째 값은 부르는 부모값, 두번째 값은 매개변수
      this.$emit("child-clicked", { name: this.name, age: this.age });
    },
  },
  // method나 mounted가 적는 순서는 상관없지만 mehods 다음에 mounted적으면 편하게 찾을 수 있다
  mounted() {
    // template에 정의된 html코드가 랜더링된 후 실행
    console.log(this);
    this.$parent.msg = "부모 컴포넌트";
  },
};
</script>

<style scoped>
/*  */
.child-container {
  border: 2px dotted red;
}
</style>
