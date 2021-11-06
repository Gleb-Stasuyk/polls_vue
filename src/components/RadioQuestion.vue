<template>
    <div class="radioQ">
          <label>{{question.question_text}} </label>
          <div v-for="choice in question.choices"
          :key="choice.id"
          :class="{ content : true }"
          >
              <input type="radio" :id="choice.id" v-model="radio_choice" :value="choice.id">
              <label>{{choice.text}}</label>
              <br>
          </div>
          <div class="buttons">
              <button 
              class="button"
              @click.prevent="sendChoice"
              >Submit</button>
          </div>
  </div>
</template>

<script>
export default {
  name: 'radio-question',
  data() {
    return {
      radio_choice: [],
      question_id: this.question.id,
      correct_choices: [],
      errorClass: 'text-danger',
      activeClass: 'active',
    }
  },
  props: {
    question: Object
  },
  mounted() {
      this.getCorrect()  
  },
  methods: {
    sendChoice () {
      this.correct_choices.includes(this.radio_choice) ? alert('Вы ответили верно') : alert('Вы ответили неверно')  
      this.$emit('send-choice', {'question_id' :this.question_id, 'choices': [this.radio_choice]})
    },
    getCorrect()  {
        this.question.choices.forEach(element => element.is_correct && this.correct_choices.push(element.id));
    }
  }
}
</script>