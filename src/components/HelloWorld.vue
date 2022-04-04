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
      <span :title="messege">올려두면 정보를 띄웁니다.</span>
      <div :id="dynamicId">qwer</div>
      <button :disabled="isButtonDisabled">Button</button>
    </div>
    <div>
      {{ name }}
      <button @click="setReverseName()">reverse name</button>
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
    <div>
      <!--
        디렉티브
        v-로 시작하는 특수한 속성입니다. 디렉티브 속성 값은 단일 JavaScript 표현식이 됩니다.
        (나중에 설명할 v-for와 v-on은 예외입니다.)
        디렉티브의 역할은 표현식의 값이 변경될 때 발생하는 부수 효과(side effects)들을 반응적으로 DOM에 적용하는 것입니다.

        v-if 디렉티브는 표현식 값의 참, 거짓 여부를 바탕으로 엘리먼트를 삽입하거나 제거합니다.
      -->
      <a :href="url"> ... </a>
      <!--
        일부 디렉티브는 디렉티브명 뒤에 콜론(:)으로 표기되는 전달인자를 가질 수 있습니다. 예를 들어, v-bind 디렉티브는 반응적으로 HTML 속성을 갱신하는 데 사용합니다.
        여기서 href는 전달인자로, v-bind 디렉티브가 표현식 url의 값을 엘리먼트의 href 속성에 바인딩하도록 지시합니다.

        또 다른 예로는 DOM 이벤트를 수신하는 v-on 디렉티브가 있습니다.

        JavaScript 표현식을 대괄호로 묶어 디렉티브 전달인자로 사용할 수도 있습니다.
      -->
      <a :[attributeName]="url"> ... </a>
    </div>
    <div>
      <!--
        약어
        v- 접두어는 템플릿에서 Vue 특정 속성을 식별하기 위한 시각적 신호 역할을 합니다.
        이 기능은 Vue.js를 사용하여 기존 마크업에 동적인 동작을 적용할 때 유용하지만,
        일부 자주 사용되는 디렉티브에 대해 장황하다고 느껴질 수 있습니다.

        v-bind와 v-on은 특별한 약어를 제공합니다.
      -->
      <!-- 약어 -->
      <a :href="url"> ... </a>
      <!-- 약어 -->
      <a @click="doSomething"> ... </a>
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
      url: `#`,
      attributeName: `href`,
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
