<template>
    <Question :title="title" :description="description" :input-example="inputExample" :output-example="outputExample"
        :input-array="inputArray" :answer-array="answerArray" :answer-function="answerFunction"
        :img-url="'src/assets/q2.jpg'" @go-to-next="goToNext" />
</template>

<script setup lang="ts">
import { reactive, ref, computed, onMounted, watch } from 'vue'
import Question from "@/components/question/Question.vue"

const title = '2. 從1數到...多少呢？'
const description = '睡不著的時候開始數數字...，數著數著，就累了，何不叫電腦幫你數呢？\n這題程式會給你一個數字，你只要回傳從1開始數到那個數字為止(包含該數字)的結果即可，例如，程式給你 ["5"]，你就要回傳 "1,2,3,4,5"，程式給你 ["1"]，你就要回傳 "1"，程式不會給你小於1的數字'
const inputExample: Array<Array<string>> = [['1'],['5'], ['20',]];
const outputExample: string[] = ['1','1,2,3,4,5', '1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20'];
const inputArray: Array<Array<string>> = [['1'],['5'], ['20'], ['17']];
const answerArray: string[] = ['1','1,2,3,4,5', '1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20', '1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17'];
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