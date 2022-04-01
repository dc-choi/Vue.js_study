<template>
  <div class="hello">
    <div>
      {{ count }}
    </div>
    <div>
      <span v-bind:title="messege">올려두면 정보를 띄웁니다.</span>
    </div>
    <div>
      {{ name }}
      <button v-on:click="setReverseName()">reverse name</button>
    </div>
    <div>
      {{ data }}
      <input v-model="data" />
    </div>
    <div>
      <span v-if="seen">나를 볼 수 있어요.</span>
    </div>
    <div>
      <ol>
        <li :key="todo" v-for="todo in todos">
          {{ todo.text }}
        </li>
      </ol>
    </div>
    <div>
      {{ msg }}
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      count: 0,
      name: "choi dong chul",
      messege: `이페이지는 ${new Date().toString()}에 랜더링 되었습니다.`,
      data: "data",
      seen: true,
      todos: [
        { text: "Learn JavaScript" },
        { text: "Learn Vue" },
        { text: "Build something awesome" },
      ],
    };
  },
  methods: {
    setReverseName() {
      this.name = this.name.split("").reverse().join("");
    },
  },
  mounted() {
    setInterval(() => {
      this.count++;
    }, 1000);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  scroll-margin: unset;
}
</style>
