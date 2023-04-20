<template>
    <Question :title="title" :description="description" :input-example="inputExample" :output-example="outputExample"
        :input-array="inputArray" :answer-array="answerArray" :answer-function="answerFunction"
        :img-url="'src/assets/q4.jpg'" @go-to-next="goToNext" />
</template>

<script setup lang="ts">
import { reactive, ref, computed, onMounted, watch } from 'vue'
import Question from "@/components/question/Question.vue"

const title = '4. 剪刀～石頭～布～'
const description = '加數字太無聊了！ 貓貓決定去找朋友玩猜拳，但朋友覺得麻煩，想要一把定勝負，為了讓遊戲時間盡可能延長，眼力超強的貓貓決定每把都出和朋友一樣的拳！！ 這樣遊戲就能一直進行下去～ 但還是怕朋友太累，決定在第20次的時候故意輸掉！ (朋友很有耐心，不會中途不玩)\n這題程式會給你一連串朋友即將出的拳，你要回傳你這邊要出的一連串的拳，要一直維持平手直到第20次的時候輸掉(格式參照範例)'
const inputExample: Array<Array<string>> = [['剪石布剪石布剪石布剪剪石布剪石布剪石布剪'],['布布布布布布布布布布布布布布布布布布布布']];
const outputExample: string[] = ['剪石布剪石布剪石布剪剪石布剪石布剪石布布','布布布布布布布布布布布布布布布布布布布石'];
const inputArray: Array<Array<string>> = [['剪石布剪石布剪石布剪剪石布剪石布剪石布剪'],['布布布布布布布布布布布布布布布布布布布布','剪剪剪剪石剪剪石石布布石石剪布石布布石石','剪剪剪布布剪剪剪剪石石剪布剪布布布剪布布']];
const answerArray: string[] = ['剪石布剪石布剪石布剪剪石布剪石布剪石布布','布布布布布布布布布布布布布布布布布布布石','剪剪剪剪石剪剪石石布布石石剪布石布布石剪','剪剪剪布布剪剪剪剪石石剪布剪布布布剪布石'];
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