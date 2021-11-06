<template>
    <div class="radioQ">
        <form>
            <label> {{question.question_text}} </label>
            <div v-for="choice in question.choices"
            :key="choice.id"
            :class="{ content : true }"
            >
                <input type="checkbox" :id="choice.id" v-model="checkbox_choice" :value="choice.id">
                <label>{{choice.text}}</label>
                
            </div>
            <div>
                <button @click.prevent="sendChoices">Отправить</button>
            </div>
        </form>
  </div>
</template>

<script>
export default {
  name: 'checkbox-question',
  data() {
    return {
      checkbox_choice: [],
      question_id: this.question.id
    }
  },
  props: {
    question: Object
  },
  methods: {
    sendChoices () {
      this.$emit('send-choices', {'question_id' :this.question_id, 'choices': this.checkbox_choice})
    }
  }
}
</script>