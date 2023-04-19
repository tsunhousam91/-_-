<template>
    <div class="question-root">
        <div class="title">{{ title }}</div>
        <div v-show="imgUrl"><img alt="" width="180" :src="imgUrl"></div>
        <div class="label">問題描述：</div>
        <div class="description">{{ description }}</div>
        <div class="label">輸入輸出範例：</div>
        <div v-for="(inputItem, index) in inputExample" :key="index" class="example">
            {{ `輸入: ${inputItem} &nbsp&nbsp&nbsp&nbsp&nbsp 回傳: ${outputExample[index]}` }}

        </div>

        <div class="label" style="margin-top:20px">您的分數：</div>
        <div class="score">
            <div v-if="score < 0">
                尚未評分
            </div>
            <div v-else-if="score < 100" style="color:red; ">
                {{ `${score}分` }}
            </div>
            <div v-else style="color:blue">
                {{ `100分 (恭喜通過！！)` }}
            </div>

        </div>

        <div class="button-region">
            <button class="button" style="color:blue" @click="sendAnswer">送出答案</button>
            <button v-if="score<100" class="button" style="color:red" @click="goToNext">窩放棄，下一題～</button>
            <button v-else class="button" style="color:blue" @click="goToNext">恭喜通過，下一題～</button>
        </div>
    </div>
</template>

<script setup lang="ts">
import { reactive, ref, computed, onMounted, watch } from 'vue'

const score = ref<number>(-100);

const props = defineProps<{
    title: string,
    imgUrl: string,
    description: string,
    inputExample: Array<Array<string>>,
    outputExample: string[],
    inputArray: Array<Array<string>>,
    answerArray: string[],
    answerFunction: Function,
}>()

const emit = defineEmits<{
  (e: 'goToNext'): void
}>()

function sendAnswer() {
    const difference: number = 100 / props.answerArray.length ;
    let tempScore: number = 100;
    for (var i: number = 0; i < props.inputArray.length; i++) {
        const yourAnswer = props.answerFunction(props.inputArray[i]);
        if (yourAnswer != props.answerArray[i]) {
            console.log(`第 ${i} 個測資錯囉，正確答案是 ${props.answerArray[i]} ，您的答案是 ${yourAnswer}`)
            tempScore -= difference;
        }
    }
    score.value = Math.round(tempScore);
}

function goToNext() {
    emit('goToNext')
}

</script>

<style lang="scss" scoped>
.question-root {
    width: calc(100% - 20px);
    height: 100%;
    border: solid black 1px;
    padding: 10px 10px;

    .title {
        font-size: 24px;
        color: blue;
        font-weight: 700;
        margin-bottom: 20px;
    }

    .img {
        width: 100px;
        height: 100px;
    }

    .label {
        font-size: 20px;
        font-weight: 700;
    }

    .description {
        font-size: 18px;
        margin-bottom: 20px;
        white-space: pre-wrap;
    }

    .example {
        font-size: 18px;
    }

    .score {
        font-size: 18px;

    }

    .button-region {
        margin-top: 20px;

        .button {
            display: inline-block;
            margin-right: 20px;
            padding: 5px 10px;
            font-size: 18px;
        }

    }

}
</style>