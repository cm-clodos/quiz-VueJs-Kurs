<template>
    <div class="result">
        <div class="title">{{ results[resultIndex].title }}</div>
        <div class="desc">
            {{ results[resultIndex].desc }}
        </div>
    </div>
</template>

<script>
export default {
    name: 'Result',
    props: {
        results: {
            type: Array,
            required: true
        },
        correctAnswers: {
            type: Number,
            required: true
        }
    },
    computed: {
        resultIndex() {
            if (this.correctAnswers <= 2) {
                return 0
            }
            else {
                return 1

            }
        }
    }

}
</script>

<style></style>