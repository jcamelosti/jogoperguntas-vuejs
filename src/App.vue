<template>
  <div>
    <template v-if="this.answers">

      <h1 v-html="this.question"></h1>
  
      <template v-for="(answer, index) in this.answers" v-bind:key="index">
        <input type="radio" name="options" value="True" />
        <label v-html="answer"></label><br />
      </template>
  
      <button class="send" type="button">Send</button>

    </template>
  </div>
</template>

<script>
export default {
  name: 'App',
  components:[],
  data(){
    return {
      question: undefined,
      incorrectAnswer: undefined,
      correctAnswer: undefined,
    }
  },  
  computed: {
    answers(){
      let answers = JSON.parse(JSON.stringify(this.incorrectAnswer));
      answers.splice(Math.round( Math.random() * answers.length),0,this.correctAnswer);
      return answers;
    }
  },
  created(){
    this.axios.get('https://opentdb.com/api.php?amount=1&category=18')
    .then((response) => {
      this.question = response.data.results[0].question;
      this.incorrectAnswer = response.data.results[0].incorrect_answers;
      this.correctAnswer = response.data.results[0].correct_answer;
    })
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 960px;

}

h1 {
  margin-top: 40px;
}

input[type='radio']{
  margin: 12px 4px;
}

button.send {
  margin-top: 12px;
  height: 40px;
  min-width: 120px;
  padding: 0 16px;
  color: #fff;
  background-color: #1867c0;
  border: 1px solid #1867c0;
  cursor: pointer;
}

section.score {
  border-bottom: 1px solid black;
  padding: 24px;
  font-size: 18px;

  span {
    padding: 8px;
    font-weight: bold;
    border: 1px solid black;
  }
}
</style>
