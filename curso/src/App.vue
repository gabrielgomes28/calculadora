<script setup>

</script>

<template>
  <div class="display">{{ current || '0' }}</div>
<div class="calculadora">
<div @click="clear" class="btn">c</div>
<div @click="sing" class="btn">+/-</div>
<div @click="percent" class="btn">%</div>
<div @click="dividir" class="btn-operador">/</div>
<div @click="append ('1')" class="btn">7</div>
<div @click="append ('2')" class="btn">8</div>
<div @click="append ('3')" class="btn">9</div>
<div @click="multiplicar" class="btn-operador">*</div>
<div @click="append ('4')" class="btn">4</div>
<div @click="append ('5')" class="btn">5</div>
<div @click="append ('6')" class="btn">6</div>
<div @click="diminuir" class="btn-operador">-</div>
<div @click="append ('1')" class="btn">1</div>
<div @click="append ('2')" class="btn">2</div>
<div @click="append ('3')" class="btn">3</div>
<div @click="somar" class="btn-operador">+</div>
<div @click= "append ('0')" class="zero">0</div>
<div @click="dot" class="btn-operador">.</div>
<div @click="igual " class="btn-operador">=</div>
</div>
   
</template>
<script>
export default{
  data(){
    return{
previous:null,
      current: '',
      operador:null,
operatorclicked:false,


      
      clear(){
        this.current='';
      },
      sing(){
        this.current=this.current.charAt(0)==='-'?
        this.current.slice(1) : `-${this.current}`;
      },
      percent(){
this.current=`${parseFloat(this.current)/100}`
      },

      append(number){
        if(this.operatorclicked){
          this.current='';
          this.operatorclicked=false;
        }
        this.current=`${this.current}${number}`;

      },

      dot(){
        if(this.current.indexOf('0')===-1){
          this.append('.');

        }
      },
    setPrevious(){
this.previous=this.current;
this.operatorclicked=true;
    },

      
      dividir(){
        this.operator=(a,b) => a/b;
this.setPrevious();
      },

      multiplicar(){
        this.operator=(a,b) => a*b;
        this.setPrevious();
      },
      somar(){
        this.operator=(a,b) => a+b;
        this.setPrevious();
      },

      diminuir(){
        this.operator=(a,b) => a-b;
        this.setPrevious();
      },
      igual(){
this.current=`${this.operator(
parseFloat(this.current),
parseFloat(this.previous)
)}`;

this.previous=null
      }
    
       
    }
  }
}
</script>
<style scoped>
.calculadora{
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px,auto);

}
.display{
  grid-column: 1/5;
  background-color: white;
}
.btn,.zero
{
  background-color: gray;
  border: 1px solid #333;
}
.btn-operador{
  background-color: orange;
  border: 1px solid #333;
}

</style>
