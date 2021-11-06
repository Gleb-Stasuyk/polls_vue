<template>
    <div class="textQ">
        <form @submit.prevent>
            <label for="GET-name">{{question.question_text}}</label>
            <input id='text-input' v-model="text"/>
            <button @click="sendAnswer">Отправить</button>
        </form>
  </div>
</template>


<script>
export default {
  name: 'text-question',
  data() {
    return {
        text: '',
        question_id: this.question.id,
    }
  },
  props: {
    question: Object
  },
  methods: {
      sendAnswer() {
          this.$emit('send-answer', {'question_id' :this.question_id, 'text': this.text})
      }
    }
}
</script>
