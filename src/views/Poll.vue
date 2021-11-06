<template>
  <div class="about">
    <h1>Опрос: {{poll.title}}</h1>

    <ul id="example-1">
        <li
        v-for="question in poll.questions"
        :key="question.id"
        :class="{ content : true }"
        >
            <radio-question v-if='question.choice_type === "radio"' :question="question" @send-choice="sendAnswer"></radio-question>
            <checkbox-question v-if='question.choice_type === "checkbox"' :question="question" @send-choices="sendAnswer"></checkbox-question>
            <text-question v-if='question.choice_type === "text"' :question="question" @send-answer="sendAnswer"> </text-question>
        </li>  
    </ul>
  </div>
</template>
<script>

import axios from 'axios'
import TextQuestion from '../components/TextQuestion.vue' 
import RadioQuestion from '../components/RadioQuestion.vue'
import CheckboxQuestion from '../components/CheckboxQuestion.vue'

export default {
  components: {TextQuestion, RadioQuestion, CheckboxQuestion },
    name: 'Poll',
    data() {
        return {
            poll: {},
        }
    },
    mounted() {
        this.getPoll()
    },
    methods: {
        async getPoll() {
            const poll_id = this.$route.params.poll_id
            axios
                .get(`/api/v1/polls/${poll_id}`)
                .then(response => {
                    this.poll = response.data
                })
                .catch(error => {
                    console.log(error)
                })
                
        },
        async sendAnswer(answer) {
            axios
            .post('/api/v1/answers/', {
                    question: answer.question_id,
                    answer_text: answer.text,
                    choices: answer.choices ? answer.choices : []
                })
                .then(function (response) {
                    console.log(response);
                    console.log(answer.choices);
                })
                .catch(function (error) {
                    console.log(error);
                    console.log(answer.choices);
                });
        }
    }
}
</script>
