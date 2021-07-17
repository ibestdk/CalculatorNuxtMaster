<template>

<div class="calculator">
    <div class="display">{{calculatorValue}}</div>
    <div class="cal_body">
        <button  @click="addNumber(7)" class="btnc s_button">7</button>
        <button  @click="addNumber(8)" class="btnc s_button">8</button>
        <button  @click="addNumber(9)" class="btnc s_button">9</button>
        <button  @click="operatoradd('+')" class="btnc s_button">+</button>
        <button  @click="addNumber(4)" class="btnc s_button">4</button>
        <button  @click="addNumber(5)" class="btnc s_button">5</button>
        <button  @click="addNumber(6)" class="btnc s_button">6</button>
        <button  @click="operatoradd('-')" class="btnc s_button">-</button>
        <button  @click="addNumber(1)" class="btnc s_button">1</button>
        <button  @click="addNumber(2)" class="btnc s_button">2</button>
        <button  @click="addNumber(3)" class="btnc s_button">3</button>
        <button  @click="operatoradd('*')" class="btnc s_button">x</button>
        <button  @click="backSpace('ลบ')" class="btnc delete s_button">ลบ</button>
        <button  @click="addNumber(0)" class="btnc s_button">0</button>
        <button  @click="addDecimal('.')" class="btnc s_button">.</button>
        <button  @click="operatoradd('/')" class="btnc s_button">÷</button>
        <button  @click="clear()" class="btnc clear">เคลียร์</button>
        <button  @click="eual()" class="btnc s_button">=</button>
    </div>
    
</div>
</template>




<script>
export default {
data() {
    return {
      calculatorValue: '0',
      operator: '',
      previousCalculatorValue: '',
      operatorEnable: false
    }
  },

  methods: {
     // รวมค่าตัวเลข 
    addNumber(n){
      if(this.isOperationBtnPress){
            this.currNum = '';
            this.isOperatorBtnPress = false;
        }

      if(!isNaN(n) || n === '.'){
        
        if(this.calculatorValue == '0' && n != 0 && n != '.' || this.calculatorValue == "0" && n == 0 || this.calculatorValue == 'Invalid')
        {
          this.calculatorValue = this.calculatorValue.replace(this.calculatorValue , `${n}`);
        }
        else{
        this.calculatorValue += n + '';
        }
      }
    },
        addDecimal(){
        if(!this.calculatorValue.toString().includes('.')){
            this.calculatorValue = `${this.calculatorValue}${'.'}`;
        }
    },
    backSpace(){
      //   ลบค่าที่ละตัว
      var tempvalue = this.calculatorValue;

        if(tempvalue.length == 1){
          this.calculatorValue = '0';
        }
        else if(tempvalue.length != 1){
          this.calculatorValue = tempvalue.toString().slice(0, -1);
          // this.calculatorValue = tempvalue.substring(0,tempvalue.length-1);
        }
        else{
        
        }
        

    },
    clear(){
      //เคลียร์ตัวเลขทั้งหมด
        this.calculatorValue = '0';
    },
    operatoradd(n){
      // การใส่เครื่องหมายต่างๆ 
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
        this.operatorEnable = true;
    },
    
    eual(){
      var temp_calculatorValue = this.calculatorValue;
      switch(this.operator) {
            case '+':
            this.calculatorValue = parseFloat(this.previousCalculatorValue) + parseFloat(temp_calculatorValue);
                break;

            case '-':
            this.calculatorValue = parseFloat(this.previousCalculatorValue) - parseFloat(temp_calculatorValue);
                break;

            case '*':
            this.calculatorValue = parseFloat(this.previousCalculatorValue) * parseFloat(temp_calculatorValue);
                break;

            case '/':
            this.calculatorValue = parseFloat(this.previousCalculatorValue) / parseFloat(temp_calculatorValue);
                break;

            default:
                this.calculatorValue ='Invalid';
                break;
        }

      this.previousCalculatorValue = '';
      this.operator = '';
      this.decimalAdded = false;
    }
  }
}

</script>