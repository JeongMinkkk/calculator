<template>
 <div class="border">
    <div class="bg-white p-10 mb-5">
      <h3>퍼센트 비율 값 계산</h3>
      <input @input="bindNumber" @change="UpdateCalc" v-model="calc1" type="text" class="border rounded p-2 text-right" placeholder="전체값 100"><span class="mr-2">의</span>
      <input type="text" class="border rounded p-2 text-right" placeholder="비율 값 20" v-model="calc2"><span class="mr-2" >%의 값은</span>
      <input type="text" class="border rounded p-2 text-right" placeholder="일부값 20" :value="ResultCalcA" readonly><span>입니다</span>
    </div>
    <div class="bg-white p-10 mb-5">
      <h3>일정 값 비율 계산</h3>
      <input type="text" class="border rounded p-2 text-right" v-model="calc3"><span>의</span>
      <input type="text" class="border rounded p-2 text-right" v-model="calc4"><span>의 값은</span>
      <input type="text" class="border rounded p-2 text-right" v-model="ResultCalcB" readonly><span>%입니다</span>
      <span class="text-xs ml-4">소수점 자리</span>
      <select v-model="sosu">
        <option v-for="e in 5" :key="e" :value="e">{{ e }}</option>
      </select>
    </div>
    <div class="bg-white p-10 mb-5">
        <h3>기준 > 변경값 비율 계산</h3>
        <input type="text" class="border rounded p-2 text-right" v-model="calc5"><span>의</span>
        <input type="text" class="border rounded p-2 text-right" v-model="calc6"><span>의 값이 변경되면</span>
        <input type="text" class="border rounded p-2 text-right" v-model="ResultCalcC" readonly><span>입니다</span>
    </div>
    <!-- c의 업그레이드버전? -->
    <div class="bg-white p-10 mb-5 flex items-center flex-wrap">
        <h3 class="basis-full">기존 > 변경값 비율 계산</h3>
        <div>
          <input type="text" class="border rounded p-2 text-right" v-model="calc7"><span>값이</span>
          <input type="text" class="border rounded p-2 text-right" v-model="calc8"><span>% 변경될 시</span>
        </div>
        <div class="flex flex-col ml-10">
          <div>
            <span class="mr-2">증가값</span>
            <input type="text" class="border rounded p-2 text-right" v-model="ResultCalcD" readonly><span>입니다</span>
          </div>
          <div class="mt-5">
            <span class="mr-2">감소값</span>
            <input type="text" class="border rounded p-2 text-right" v-model="ResultCalcE" readonly><span>입니다</span>
          </div>
        </div>
    </div>
 </div>
</template>

<script>
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
    // 변수쓰는이유 - 이런 방법도 있다.
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
