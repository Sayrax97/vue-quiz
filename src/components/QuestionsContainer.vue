<template>
  <div>
    <b-jumbotron :header="question.question">
      <b-list-group>
        <b-list-group-item
          v-for="(quest,index) in currentQuestion"
          :key="index"
          @click="selectedIndex=index"
          :class="[!answerd && selectedIndex==index?'selected':
          answerd && correctIndex==index ? 'correct':
          answerd && correctIndex!=index ? 'wrong': ''
          ]"
        >{{quest}}</b-list-group-item>
      </b-list-group>
    </b-jumbotron>
    <b-button @click="submit" variant="primary" size="lg" :disabled="brojac==10 || submited">Sumbit</b-button>
    <b-button @click="nextClick" variant="primary" size="lg" :disabled="brojac==10">Next</b-button>
  </div>
</template>

<script>
export default {
  props: {
    question: Object,
    next: Function
  },
  methods: {
    submit: function() {
      this.answerd = true;
      this.submited = true;
      if (
        this.currentQuestion[this.selectedIndex] == this.question.correct_answer
      ) {
        this.$emit("tacan");
      } else {
      }
    },
    compareToAnswer: function(item) {
      return this.question.correct_answer == item;
    },
    nextClick: function() {
      this.next();
      this.brojac++;
      this.answerd = false;
      this.submited = false;
    }
  },
  computed: {
    currentQuestion() {
      var x = [...this.question.incorrect_answers];
      x.push(this.question.correct_answer);
      for (let i = x.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * i);
        const temp = x[i];
        x[i] = x[j];
        x[j] = temp;
      }
      this.correctIndex = x.findIndex(this.compareToAnswer);
      return x;
    }
  },
  data: function() {
    return {
      selectedIndex: "",
      answerd: false,
      correctIndex: undefined,
      brojac: 0,
      submited: false
    };
  }
};
</script>

<style scoped>
.list-group-item:hover {
  background-color: aqua;
  cursor: pointer;
  color: black;
}
.selected {
  background-color: lightblue;
  color: black;
}
.correct {
  background-color: greenyellow;
  color: black;
}
.wrong {
  background-color: red;
  color: white;
}
</style>