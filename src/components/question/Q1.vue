<template>
    <Question :title="title" :description="description" :input-example="inputExample" :output-example="outputExample"
            :input-array="inputArray" :answer-array="answerArray" :answer-function="answerFunction"
            :img-url="'src/assets/q1.jpg'" @go-to-next="goToNext"/>
</template>

<script setup lang="ts">
import { reactive, ref, computed, onMounted, watch } from 'vue'
import Question from "@/components/question/Question.vue"

const title = '1. 君の名前は'
const description = '你忘記了自己的名字，別擔心，程式會幫你想起來！\n這題程式會給你兩個資料，第一個是你的年紀，第二個是你的名字，你只要正確地回傳你的名字跟歲數即可，例如，如果程式給你 ["12","禰豆子"]，那你必須回傳 "我叫禰豆子,今年12歲"'
const inputExample: Array<Array<string>> = [['5', '薯片'], ['12', '禰豆子']];
const outputExample: string[] = ['我叫薯片,今年5歲', '我叫禰豆子,今年12歲'];
const inputArray: Array<Array<string>> = [['5', '薯片'], ['12', '禰豆子'], ['18', '彤語']];
const answerArray: string[] = ['我叫薯片,今年5歲', '我叫禰豆子,今年12歲', '我叫彤語,今年18歲'];
defineProps<{
    answerFunction: Function
}>()
const emit = defineEmits<{
  (e: 'goToNext'): void
}>()
function goToNext() {
    emit('goToNext')
}

</script>

<style scoped></style>