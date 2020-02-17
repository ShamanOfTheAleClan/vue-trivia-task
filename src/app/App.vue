<template>
  <div id="app">
    <main
      class="main"
    >

    <QuizButton
      v-if="isGameStart"
      button-text="Start game"
      @click="startGame"
    >
    </QuizButton>

    <Surface
      v-if="!isGameStart && !gameOver"
    >
      <span v-if="isRequesting && score===0">Get ready!</span>
      <span v-if="isRequesting && score>0">Nooice!</span>
      <template v-if="currentQuestion && !isRequesting">
        <Timer>
        </Timer>
        <h4>
          {{ currentQuestion.category }}
        </h4>
        <h1>
          {{ currentQuestion.question }}
        </h1>
        <ul class="list">
          <li
            v-for="answer in currentAnswers"
            :key="answer"
            class='list-item'
          >
            <QuizButton
              class='button'
              :outlined='true'
              :button-text="answer"
              @click='checkAnswer(answer)'
            >
            </QuizButton>

          </li>
        </ul>
      </template>
    </Surface>

    <template
      v-if="gameOver"
    >
      <Surface>
        Your score: {{ score }}
      </Surface>
      <QuizButton
        class="button"
        button-text="Play again"
        @click='startGame'
      >
      </QuizButton>
    </template>
    </main>
  </div>
</template>

<script>
import axios from '@/packages/axios'
import QuizButton from '../components/QuizButton.vue'
import Surface from '../components/Surface'
import Timer from '../components/Timer'
export default {
  name: 'App',
  components: {
    QuizButton,
    Surface,
    Timer
  },
  data () {
    return {
      isRequesting: false,
      isGameStart: true,
      currentIndex: 0,
      questions: [],
      score: 0,
      gameOver: false
    }
  },
  computed: {
    currentQuestion () {
      if (this.questions.length) {
        return this.questions[this.currentIndex]
      }
      return null
    },
    currentAnswers () {
      const { currentQuestion } = this
      if (currentQuestion) {
        return this.shuffle([
          ...currentQuestion.incorrect_answers,
          currentQuestion.correct_answer
        ])
      }
      return []
    }

  },
  methods: {
    async fetchQuestions () {
      this.isRequesting = true
      try {
        const { data } = await axios.get('/api.php?amount=1')
        this.questions = data.results
        this.isRequesting = false
      } catch (error) {
        this.isRequesting = false
      }
    },
    shuffle (e) {
      const array = [...e]
      const output = []
      for (let i = 0; i < e.length; i++) {
        const rng = Math.floor(Math.random() * Math.floor(array.length))
        output.push(array.splice(rng, 1)[0])
      }
      return output
    },
    startGame () {
      this.isGameStart = false
      this.gameOver = false
      this.fetchQuestions()
      this.score = 0
    },
    checkAnswer (e) {
      if (e === this.currentQuestion.correct_answer) {
        this.fetchQuestions()
        this.score++
      } else {
        this.gameOver = true
      }
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}

.main {
  background-color: #782aac;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  height: 100vh;
  box-sizing: border-box;
}

.list {
  padding: 0;
}

.list-item {
  list-style: none;
}

</style>
