<template>
  <div>
    <h3>{{ msg }}</h3>
    <table>
      <thead>
        <tr>
          <th>아이디</th>
          <th>이름</th>
          <th>나이</th>
        </tr>
      </thead>
      <tbody>
        <!-- 반복문 데이터라는놈이 가지고 있음 -->
        <tr v-bind:key="i" v-for="(prod, i) in data">
          <!-- (prod, i) i의 두번째값 인덱스? id를 키로 생각하면 뭔소리야 prod안에는 id도 있고 name도 있고 -->
          <td>{{ prod.id }}</td>
          <td v-text="prod.name"></td>
          <td>{{ prod.age }}</td>
        </tr>
      </tbody>
    </table>
    <table>
      <thead>
        <tr>
          <th>카테고리</th>
          <th>배달가격</th>
          <th>가격</th>
          <th>이름</th>
        </tr>
      </thead>
      <tbody>
        <!-- 반복문 데이터라는놈이 가지고 있음 -->
        <tr v-bind:key="i" v-for="(prod, i) in prodList">
          <!-- (prod, i) i의 두번째값 인덱스? id를 키로 생각하면 뭔소리야 prod안에는 id도 있고 name도 있고 -->
          <td>{{ prod.category }}</td>
          <td v-text="prod.delivery_price"></td>
          <td>{{ prod.price }}</td>
          <td>{{ prod.product_name }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "학생목록",
      data: [
        { id: 1, name: "홍길동", age: 20 },
        { id: 2, name: "김민수", age: 22 },
        { id: 3, name: "최익수", age: 23 },
      ],
      prodList: [],
    };
  },
  beforeCreate() {
    console.log("beforeCreate");
  },
  created() {
    console.log("created");
  },
  beforeMount() {
    console.log("beforeMount");
  },
  beforeUpdate() {
    // 데이터가 바뀔때마다 훅이 호출됨
    console.log("beforeUpdate");
  },
  updated() {
    // 데이터가 바뀔때마다 훅이 호출됨
    console.log("updated");
  },
  mounted() {
    // DataBindingList 컴포넌트가 생성이 되면
    fetch("http://192.168.0.8:3000/products")
      .then((response) => response.json())
      .then((result) => {
        console.log(result);
        this.prodList = result; // 데이터 변경
      });
  },
};
</script>

<style scoped></style>
