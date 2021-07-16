<template>

<div class="calculator">
    <div class="display">{{calculatorValue}}</div>
    <div class="cal_body">
        <button  @click="action('7')" class="btnc s_button">7</button>
        <button  @click="action(8)" class="btnc s_button">8</button>
        <button  @click="action(9)" class="btnc s_button">9</button>
        <button  @click="action('+')" class="btnc s_button">+</button>
        <button  @click="action(4)" class="btnc s_button">4</button>
        <button  @click="action(5)" class="btnc s_button">5</button>
        <button  @click="action(6)" class="btnc s_button">6</button>
        <button  @click="action('-')" class="btnc s_button">-</button>
        <button  @click="action(1)" class="btnc s_button">1</button>
        <button  @click="action(2)" class="btnc s_button">2</button>
        <button  @click="action(3)" class="btnc s_button">3</button>
        <button  @click="action('*')" class="btnc s_button">x</button>
        <button  @click="action('ลบ')" class="btnc delete s_button">ลบ</button>
        <button  @click="action(0)" class="btnc s_button">0</button>
        <button  @click="action('.')" class="btnc s_button">.</button>
        <button  @click="action('/')" class="btnc s_button">÷</button>
        <button  @click="action('เคลียร์')" class="btnc clear">เคลียร์</button>
        <button  @click="action('=')" class="btnc s_button">=</button>
    </div>
    
</div>
</template>




<script>
export default {
data() {
    return {
      calculatorValue: '',
      operator: null,
      previousCalculatorValue: '',
    }
  },

  methods: {
    action(n){

      // รวมค่าตัวเลข 
      if(!isNaN(n) || n === '.'){
        
        if (n === 0){
          if(this.calculatorValue === 0) {
            return this.calculatorValue = "0";
        }
        
    }
        else{
          this.calculatorValue += n + '';
        }
        

      }
      //   ลบค่าที่ละตัว
    if(n === 'ลบ'){
          this.calculatorValue = this.calculatorValue.substring(0,this.calculatorValue.length-1);
          
      }

      //เคลียร์ตัวเลขทั้งหมด
      if(n === 'เคลียร์'){
        this.calculatorValue = '';
      }

      // การใส่เครื่องหมายต่างๆ 
      if(['/','*','-','+'].includes(n)){
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
      }

      // คำนวณโดยใช้ ฟังก์ชั่นeval สรุปค่าหลังจากใส่ตัวเเปรครบเเล้ว เเละทำการเคลีย ค่าตัวเลขก่อน เเละค่าเครื่องหมาย 
      if(n === '='){
        if(this.calculatorValue === '' || this.operator === null || this.previousCalculatorValue ===''){
        }
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = '';
        this.operator = null;
      }
      


    }
  }
}
</script>