<template>
    <Question :title="title" :description="description" :input-example="inputExample" :output-example="outputExample"
        :input-array="inputArray" :answer-array="answerArray" :answer-function="answerFunction"
        :img-url="'src/assets/q2.jpg'" @go-to-next="goToNext" />
</template>

<script setup lang="ts">
import { reactive, ref, computed, onMounted, watch } from 'vue'
import Question from "@/components/question/Question.vue"

const title = '3. 數字累加，但不喜歡質數～'
const description = '貓貓數了數字還是睡不著，決定起床來練習數字累加（？？）\n就是從1開始往後加，把結果算出來就好了，成功攻略了上一題後，想必這難不倒各位，不過呢，貓咪不喜歡質數！ 所以遇到質數就不加！(質數是只能被1和自己整除的數字，但1跟2不是質數)\n這題程式會給你一個數字，請你累加到該數字(包含該數字)，但遇到質數請忽略，例如，程式給你 ["8"]，請回傳 1+2+4+6+8 的結果，也就是回傳 21'
const inputExample: Array<Array<string>> = [['1'],['2'], ['8']];
const outputExample: string[] = ['1','3', '21'];
const inputArray: Array<Array<string>> = [['1'],['2'], ['8'],['15'],['105'],['215'],['123'],['1024']];
const answerArray: string[] = ['1','3', '21','81','4303','18784','6035','444613',];
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