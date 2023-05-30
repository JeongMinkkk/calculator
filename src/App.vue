<template>
 <div class="p-[2%] bg-black">
  <div class="border bg-white rounded-md">
    <div class="">
      <div class="flex justify-center">
        <lottie-player :src="require('@/assets/90332-saas-black-and-white.json')" background="transparent" speed="1" style="max-width: 150px; max-height: 150px;" autoplay loop></lottie-player>
        <p class="text-2xl font-bold text-center mt-9 md:text-5xl ">퍼센트계산기</p>
      </div>
    </div>
    <!-- 퍼센트 비율 값 계산 -->
    <div class="bg-white p-10 mb-5">
      <h3 class="text-xl border-b-4 mb-2 border-yellow-300 text-center mx-10 md:mx-20">퍼센트 비율 값 계산</h3>
      <div class="sm:text-center">
        <input @input="bindNumber" @change="UpdateCalc" v-model="calc1" type="text" class="border rounded p-2 text-right mb-1" placeholder="전체값 100"><span class="mr-2">의</span>
        <input type="text" class="border rounded p-2 text-right mb-1" placeholder="비율 값 20" v-model="calc2"><span class="sm:mr-2">% 는</span>
        <input type="text" class="border rounded p-2 text-right mb-1" placeholder="일부값 20" :value="ResultCalcA" readonly><span>입니다</span>
      </div>
    </div>
    <!-- 일정 값 비율 계산 -->
    <div class="bg-white p-10 mb-5">
      <h3 class="text-xl border-b-4 mb-2 border-yellow-300 text-center mx-10 md:mx-20">일정 값 비율 계산</h3>
      <div class="sm:text-center">
        <input type="text" class="border rounded p-2 text-right mb-1" placeholder="전체값 100" v-model="calc3"><span class="sm:mr-2">에서</span>
        <input type="text" class="border rounded p-2 text-right mb-1" placeholder="비율 값 20" v-model="calc4"><span  class="sm:mr-2">은(는)</span>
        <input type="text" class="border rounded p-2 text-right mb-1" placeholder="일부값 20" v-model="ResultCalcB" readonly><span>입니다</span>
        <span class="text-xs ml-2 mr-1">소수점 자리</span>
        <select v-model="sosu">
          <option v-for="e in 5" :key="e" :value="e">{{ e }}</option>
        </select>
      </div>
    </div>
    <!-- 기준 > 변경값 비율 계산 -->
    <div class="bg-white p-10 mb-5">
        <h3 class="text-xl border-b-4 mb-2 border-yellow-300 text-center mx-7 sm:mx-10 md:mx-20">기준 > 변경값 비율 계산</h3>
        <div class="sm:text-center">
          <input type="text" class="border rounded p-2 text-right mb-1" placeholder="기준값 100" v-model="calc5"><span class="sm:mr-2">이(가)</span>
          <input type="text" class="border rounded p-2 text-right mb-1" placeholder="변경값 150" v-model="calc6"><span class="sm:mr-2">의 값이 변경되면</span>
          <input type="text" class="border rounded p-2 text-right mb-1" placeholder="증가값 50" v-model="ResultCalcC" readonly><span>입니다</span>
        </div>
    </div>
    <!-- 기존 > 변경값 비율 계산 -->
    <div class="bg-white p-10 mb-5 flex items-center flex-wrap justify-center">
      <h3 class="basis-full text-xl border-b-4 mb-2 border-yellow-300 text-center mx-7 sm:mx-10 md:mx-20">기존 > 변경값 비율 계산</h3>
      <div>
        <input type="text" class="border rounded p-2 text-right mb-1" placeholder="기준값 100" v-model="calc7"><span class="sm:mr-2">이(가)</span>
        <input type="text" class="border rounded p-2 text-right mb-1" placeholder="비율값 20" v-model="calc8"><span class="sm:mr-2">%</span>
      </div>
      <div class="flex flex-col ml-10">
        <div>
          <span class="sm:mr-2">증가하면</span>
          <input type="text" class="border rounded p-2 text-right mb-1" placeholder="변경값 120" v-model="ResultCalcD" readonly><span>입니다</span>
        </div>
        <div class="mt-5">
          <span class="sm:mr-2">감소하면</span>
          <input type="text" class="border rounded p-2 text-right mb-1" placeholder="변경값 80" v-model="ResultCalcE" readonly><span>입니다</span>
        </div>
      </div>
    </div>
  </div>
 </div>
</template>

<script>
import "@lottiefiles/lottie-player";

export default {
  name: 'App',
  data() {
    return {
      calc1:'',
      calc2:'',
      calc3:'',
      calc4:'',
      calc5:'',
      calc6:'',
      calc7:'',
      calc8:'',
      sosu:'2'
    }
  },
  methods:{
    UpdateCalc(){
      console.log("1111")
    },
    bindNumber(e){
      this.calc1 = e.target.value;
    }
  },
  // 연산자.이벤트 
  computed:{
    ResultCalcA(){
      return this.calc2 === '' || this.calc1 === '' ? '': (Number(this.calc1) * Number((this.calc2/100))).toFixed(3)
    },
    ResultCalcB(){
      return this.calc4 === '' || this.calc3 === '' ? '' : ((100 * Number(this.calc4)) / Number(this.calc3)).toFixed(this.sosu)
    },
    ResultCalcC(){
      let a = (this.calc6 - this.calc5) / this.calc5 * 100;
      return this.calc6 === '' || this.calc5 === '' ? '' : a > 0 ? a.toFixed(0)+"% 증가" : a.toFixed(0)+"% 감소"
    },
    ResultCalcD(){
      return this.calc7 === '' || this.calc8 === '' ? '' : (Number(this.calc7) + Number(this.calc7) * Number(this.calc8 / 100)).toFixed(0)
    },
    ResultCalcE(){
      return this.calc7 === '' || this.calc8 === '' ? '' : (Number(this.calc7) - Number(this.calc7) * Number(this.calc8 / 100)).toFixed(0)
    }
  },
  // 숫자만 입력해야해서.감시함
  watch:{
    calc1: function(){
      return this.calc1 = this.calc1.replace(/[^0-9]/g,'')
    },
    calc2: function(){
      return this.calc2 = this.calc2.replace(/[^0-9]/g,'')
    }

  },
  components: {
  },
}
</script>

<style>
@font-face {
    font-family: 'GmarketSansMedium';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2001@1.1/GmarketSansMedium.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}
*{font-family: 'GmarketSansMedium';}
</style>
