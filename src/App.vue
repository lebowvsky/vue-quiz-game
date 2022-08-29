<template>
  <div>
    <template v-if="this.question">
      <h1 v-html="this.question"></h1>
      <template v-for="answer in this.answers" :key="answer">
        <input
          type="radio"
          name="options"
          :value="answer"
          v-model="this.chosenAnswer"
          :disabled="this.answerSubmited"
        />
        <label v-html="answer"></label>
        <br />
      </template>

      <button class="send" type="button" @click="submitAnswer()" v-if="!this.answerSubmited">Send</button>

      <section v-if="this.answerSubmited" class="result">
        <h4 v-if="this.chosenAnswer == this.correctAnswer">&#9989; Congratulation, the answer is good !!!</h4>
        <h4 v-else>&#10060; I'm sorry, youpicked the wrong answer. The correct answer was {{ this.correctAnswer }}</h4>
        <button class="send">NextQuestion</button>
      </section>
    </template>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswer: undefined,
      chosenAnswer: undefined,
      answerSubmited: false,
    };
  },
  computed: {
    answers() {
      let answers = [...this.incorrectAnswers];
      answers.push(this.correctAnswer);
      return answers.sort(() => Math.random() - 0.5);
    },
  },
  methods: {
    submitAnswer() {
      if (!this.chosenAnswer) {
        alert("Chose an answer !");
      } else {
        if (this.chosenAnswer === this.correctAnswer) {
          this.answerSubmited = true;
        } else {
          this.answerSubmited = true;
        }
      }
    },
  },
  async created() {
    const response = await this.axios.get("https://opentdb.com/api.php?amount=1&category=18");
    this.question = response.data.results[0].question;
    this.incorrectAnswers = response.data.results[0].incorrect_answers;
    this.correctAnswer = response.data.results[0].correct_answer;
  },
};
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  input {
    margin: 15px 10px 0 0;
  }

  button {
    background-color: rgb(135, 135, 230);
    color: white;
    border: none;
    padding: 8px 20px;
    margin: 20px 0 0 0;
    cursor: pointer;
  }
}
</style>
