<template>
  <div class="hello">
    <!--
      문자열 보간법 {{}}
      이중 중괄호는 데이터를 HTML이 아닌 일반 텍스트로 해석합니다.
      웹사이트에서 임의의 HTML을 동적으로 렌더링하면 XSS 취약점으로 쉽게 이어질 수 있고 이는 매우 위험할 소지가 있습니다.
      HTML 보간법은 반드시 신뢰할 수 있는 콘텐츠에서만 사용하고 사용자가 제공한 콘텐츠에서는 절대 사용하면 안 됩니다.
      이중 중괄호는 HTML 속성에 사용할 수 없습니다. 대신 v-bind 디렉티브를 사용하세요.
    -->
    <div>
      {{ count }}
    </div>
    <div>
      <span v-bind:title="messege">올려두면 정보를 띄웁니다.</span>
      <div v-bind:id="dynamicId">qwer</div>
      <button v-bind:disabled="isButtonDisabled">Button</button>
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
    <div>
      <span v-once>결코 변하지 않을 것입니다: {{ data }}</span>
    </div>
    <div>
      <p>v-html 디렉티브 사용: <span v-html="rawHtml"></span></p>
    </div>
    <!-- {{}} 안에 JS 표현식으로 사용 가능 -->
    <div>
      {{ number + 1 }}
      {{ ok ? "YES" : "NO" }}
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
      rawHtml: `<span style="color: red">This should be red.</span>`,
      dynamicId: `hi`,
      isButtonDisabled: true, // null, undefined
      number: 1,
      ok: true,
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
.hello {
  margin: auto;
}
</style>
