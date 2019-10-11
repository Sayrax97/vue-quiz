<template>
  <div id="app">
    <HeaderVue :p="poeni"></HeaderVue>
    <QuestionsContainerVue
      v-if="questions.length"
      :question="questions[id]"
      :next="nextQuestion"
      @tacan="tacanOdgovor"
    ></QuestionsContainerVue>
  </div>
</template>

<script>
import QuestionsContainerVue from "./components/QuestionsContainer.vue";
import HeaderVue from "./components/Header.vue";

export default {
  name: "app",
  components: {
    QuestionsContainerVue,
    HeaderVue
  },
  data: function() {
    return { questions: "", id: 0, poeni: 0 };
  },
  methods: {
    nextQuestion: function() {
      if (this.id == 9) {
        this.makeToast();
        return;
      }
      this.id++;
    },
    tacanOdgovor: function() {
      this.poeni++;
    },
    makeToast(append = false) {
      this.$bvToast.toast(`You had ${this.poeni} out of 10 questions right`, {
        title: "Congratulations",
        toaster: "b-toaster-top-center",
        autoHideDelay: 5000,
        variant: "primary",
        appendToast: append
      });
    }
  },
  mounted() {
    fetch("https://opentdb.com/api.php?amount=10&category=18&type=multiple", {
      method: "GET"
    })
      .then(response => response.json())
      .then(jsonData => {
        this.questions = jsonData.results;
      });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.btn {
  margin-right: 10px;
}
</style>
