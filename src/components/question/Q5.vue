<template>
    <Question :title="title" :description="description" :input-example="inputExample" :output-example="outputExample"
        :input-array="inputArray" :answer-array="answerArray" :answer-function="answerFunction"
        :img-url="''" @go-to-next="goToNext" />
</template>

<script setup lang="ts">
import { reactive, ref, computed, onMounted, watch } from 'vue'
import Question from "@/components/question/Question.vue"

const title = '5. 來排序吧'
const description = '排序是寫程式很可能碰到的問題，來練習一下吧～ \n這題程式會給一連串的資料，可能是阿拉伯數字或普通文字，如果是數字請由小到大排序，如果是文字請把他剔除，但如果文字是 "零一二三四五六七八九" 裡的文字組成的資料，請不要剔除並當成數字由小到大排列(但保留文字型態)，若出現相同值的阿拉伯數字跟普通文字，則阿拉伯數字先排，普通文字放在後面，如果資料同時包含阿拉伯數字以及"零一二三四五六七八九"裡的資料，請把他剔除，另外開頭的0或"零"不需要出現在排序結果裡(排序結果要拿掉開頭的0跟零)，排序結果用","隔開 (程式不會給你空字串的資料)'
const inputExample: Array<Array<string>> = [['1','03','00110','哈囉','喔喔','1零34','72','零三五','零零三五八'],['000','零零零','2','二','2','零一一','三三零三','00017','一七零','0']];
const outputExample: string[] = ['1,3,三五,72,110,三五八','0,0,零,2,2,二,一一,17,一七零,三三零三'];
const inputArray: Array<Array<string>> = [['1','03','00110','哈囉','喔喔','1零34','72','零三五','零零三五八'],['000','零零零','2','二','2','零一一','三三零三','00017','一七零','0'],['零1五五','0012五','00000012','12','1212','12','零零零','零零一二','零一二零','假資料']];
const answerArray: string[] = ['1,3,三五,72,110,三五八','0,0,零,2,2,二,一一,17,一七零,三三零三','零,12,12,12,一二,一二零,1212'];
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