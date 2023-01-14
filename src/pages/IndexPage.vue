<template>
  <q-page class="flex flex-center ">
    <q-card class="q-ma-sm column" flat>
      <div class="q-ma-xl">
        <div class="col-1 text-weight-bold text-h6">진수 변환기</div>
        <div class="col-1 q-mt-sm" style="color: grey">2진수, 8진수, 10진수, 16진수를 상호 변환해 줍니다</div>
        <q-form class="col-8 q-mt-xl q-mb-xl">
          <q-input label="입력" v-model="input" outlined class="q-mb-lg" maxlength=30 :rules=inputRule />
          <div class="row justify-around q-mb-xl">
            <q-select transition-show="flip-up" transition-hide="flip-down" dense outlined v-model="from" :options="binary"></q-select>
            <div class="q-ma-sm">에서</div>
            <q-select transition-show="flip-up" transition-hide="flip-down" dense outlined v-model="to" :options="binary"></q-select>
            <div class="q-ma-sm">(으)로</div>
            <q-btn style="height: 30px" push color="primary" label="변환하기" @click="calc()"/>
            <q-btn style="height: 30px" push color="grey" label="지우기" class="q-ml-sm" @click="clear()"/>
          </div>
          <q-input label="결과" v-model="result" readonly outlined autogrow />
        </q-form>
      </div>
    </q-card>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { useQuasar } from 'quasar'


export default defineComponent({
  name: 'IndexPage',

  setup() {
    const $q = useQuasar()

    let input =  ref(null)
    let result =  ref(null)
    const from = ref('10진수')
    const to = ref('2진수')
    const binary = ref(['2진수', '8진수', '10진수', '16진수'])

    var NumberSystem = require('number-system')
    let ns = new NumberSystem(10);

    function calc() {
      if (from.value === '10진수') {
        if (to.value === '2진수') {
          result.value = ns.bin(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else if (to.value === '8진수') {
          result.value = ns.oct(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else if (to.value === '16진수') {
          result.value = ns.hex(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
      }
      else if (from.value === '2진수') {
        ns.base = 2
        if(to.value === '10진수'){
          result.value = ns.dec(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else if (to.value === '8진수') {
          result.value = ns.oct(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else if (to.value === '16진수') {
          result.value = ns.hex(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else {
          $q.notify({
            message: 'Error',
            color: 'negative'
          })
        }
      }
      else if (from.value === '8진수') {
        ns.base = 8
        if(to.value === '10진수'){
          result.value = ns.dec(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else if (to.value === '2진수') {
          result.value = ns.bin(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else if (to.value === '16진수') {
          result.value = ns.hex(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else {
          $q.notify({
            message: 'Error',
            color: 'negative'
          })
        }
      }
      else if (from.value === '16진수') {
        ns.base = 16
        if(to.value === '10진수'){
          result.value = ns.dec(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else if (to.value === '8진수') {
          result.value = ns.oct(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else if (to.value === '2진수') {
          result.value = ns.bin(input.value)
          $q.notify({
            message: '변환 완료',
            color: 'positive'
          })
        }
        else {
          $q.notify({
            message: 'Error',
            color: 'negative'
          })
        }
      }
      else {
        $q.notify({
            message: 'Error',
            color: 'negative'
          })
      }
    }

    function clear() {
      input.value = null
      result.value = null
      $q.notify({
        message: "지우기 완료",
        color: 'positive'
      })
    }

      return {
        calc,
        clear,
        input,
        result,
        from,
        to,
        binary,
        inputRule: [val => !!val || '입력란이 비었습니다'],
      }
  }

})
</script>
