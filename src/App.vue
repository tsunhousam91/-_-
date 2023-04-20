

<template>
  <header>

  </header>

  <main>
    <Q1 v-show="selectedQuestionNo == 1" :answer-function="answerFunction_Q1" @go-to-next="goToNext" />
    <Q2 v-show="selectedQuestionNo == 2" :answer-function="answerFunction_Q2" @go-to-next="goToNext" />
    <Q3 v-show="selectedQuestionNo == 3" :answer-function="answerFunction_Q3" @go-to-next="goToNext" />
    <Q4 v-show="selectedQuestionNo == 4" :answer-function="answerFunction_Q4" @go-to-next="goToNext" />
    <Q5 v-show="selectedQuestionNo == 5" :answer-function="answerFunction_Q5" @go-to-next="goToNext" />
  </main>
</template>

<script setup lang="ts">

import { reactive, ref, computed, onMounted, watch } from 'vue'
import Q1 from '@/components/question/Q1.vue';
import Q2 from '@/components/question/Q2.vue';
import Q3 from '@/components/question/Q3.vue';
import Q4 from '@/components/question/Q4.vue';
import Q5 from '@/components/question/Q5.vue';

const selectedQuestionNo = ref<number>(1);

function answerFunction_Q1(inputArray: Array<string>) {
  return `我叫${inputArray[1]},今年${inputArray[0]}歲`
}

function answerFunction_Q2(inputArray: Array<string>) {
  let endNumber: number = +inputArray[0];
  let result: string = '1';
  for (var i: number = 2; i <= endNumber; i++) {
    result += `,${i}`;
  }
  return result;
}

function _isPrime(n: number) {
  if (n <= 2 || n % 2 == 0) {
    return false;
  }
  let sqrt = Math.floor(Math.sqrt(n));
  for (var i = 3; i <= sqrt; i += 2) {
    if (n % i == 0) {
      return false;
    }
  }
  return true;
}

function answerFunction_Q3(inputArray: Array<string>) {
  let endNumber: number = +inputArray[0];
  let sum: number = 0;
  for (var i: number = 1; i <= endNumber; i++) {
    if (!_isPrime(i)) {
      sum += i;
    }
  }
  return sum.toString();
}

function answerFunction_Q4(inputArray: Array<string>) {
  let friendHands: string = inputArray[0];
  let myHands: string = '';
  for (var i: number = 0; i <= friendHands.length; i++) {
    if (i < 19) {
      myHands += friendHands[i];
      continue;
    }
    switch (friendHands[i]) {
      case '剪':
        myHands += '布';
        break;
      case '石':
        myHands += '剪';
        break;
      case '布':
        myHands += '石';
        break;
    }
  }
  return myHands;
}

function _isTextNumber(c: string) {
  return '零一二三四五六七八九'.includes(c);
}

function _isPureNumber(c: string) {
  return '0123456789'.includes(c);
}

/// 轉換成沒有 0或零開頭的阿拉伯數字或中文數字，異常資料會回傳空字串
function _convertToValidData(rawData: string) {
  let isPure = false; // 偵測是否為純數字
  let isText = false; // 偵測是否為文字數字
  let isHeadingZero = true; // 偵測最前面的0或零
  let result = '';
  for (var i: number = 0; i < rawData.length; i++) {
    if (_isPureNumber(rawData[i])) {
      if (isText) {
        return '';
      }
      isPure = true;
      if (rawData[i] != '0') {
        isHeadingZero = false;
      } else if (isHeadingZero) {
        continue;
      }
      result += rawData[i];
    } else if (_isTextNumber(rawData[i])) {
      if (isPure) {
        return '';
      }
      isText = true;
      if (rawData[i] != '零') {
        isHeadingZero = false;
      } else if (isHeadingZero) {
        continue;
      }
      result += rawData[i];
    } else {
      return '';
    }
  }
  if (!result) {
    return isText ? '零' : '0';
  }
  return result;
}


function _toRealNumber(convertedData: string) {
  let pureNumber = '';
  if (_isTextNumber(convertedData[0])) {
    for (var i: number = 0; i < convertedData.length; i++) {
      pureNumber += '0123456789'['零一二三四五六七八九'.indexOf(convertedData[i])];
    }
  } else {
    pureNumber = convertedData;
  }
  return +pureNumber;
}

function answerFunction_Q5(inputArray: Array<string>) {
  let validData: Array<string> = [];
  for (var i: number = 0; i < inputArray.length; i++) {
    let convertedData = _convertToValidData(inputArray[i]);
    if (convertedData) {
      validData.push(convertedData);
    }
  }
  validData.sort(function (a, b) {
    let realA: number = _toRealNumber(a);
    let realB: number = _toRealNumber(b);
    if (realA < realB) {
      return -1;
    } else if (realA > realB) {
      return 1;
    } else {
      if (_isPureNumber(a)) {
        return -1;
      } else {
        return 1;
      }
    }
  });
  return validData.join(',')
}

function goToNext() {
  if (selectedQuestionNo.value >= 5) {
    selectedQuestionNo.value = 1;
  } else {
    selectedQuestionNo.value++;
  }
}
</script>

<style scoped></style>
