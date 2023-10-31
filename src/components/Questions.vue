<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="{ width: `${(currentQuestionIndex / questions.length) * 100}%` }"></div>
            <div class="status">{{ this.currentQuestionIndex }} out of {{ this.questions.length }} questions answered</div>
        </div>
        <transition-group name="fade">
        <div class="single-question">
            <div class="question"> {{ currentQuestion.q }}</div>
            <div class="answers" v-for="(answer, index) in currentQuestion.answers" :key="index"
                @click.prevent="checkAnswer(answer.is_correct)">
                <div class="answer">{{ answer.text }}</div>
            </div>
        </div>
    </transition-group>
    </div>
</template>

<script>
export default {
    name: 'Questions',
    props: {
        questions: {
            type: Array,
            required: true
        }
    },
    emits: ['question-answered', 'correct-answers'],
    data() {
        return {
            currentQuestionIndex: 0,
            correctAnswers: 0,
        }
    },
    computed: {
        currentQuestion() {
            return this.questions[this.currentQuestionIndex]
        }
    },
    methods: {
        checkAnswer(isCorrect) {
            if (isCorrect) {
                this.correctAnswers++;
                console.log('correct');
            } else {
                console.log('wrong');
            }
            // emit der questionAnswerd event aktualsiert und an den parent schickt + die richtigen Antworten weiterleitet
            this.$emit('correct-answers', this.correctAnswers);


            this.moveToNextQuestion();
        },
        moveToNextQuestion() {
            if (this.currentQuestionIndex < this.questions.length)
                this.currentQuestionIndex++;
            this.$emit('question-answered', this.currentQuestionIndex);
        }

    }
}
</script>

<style></style>