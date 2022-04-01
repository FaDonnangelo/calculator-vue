<template>
  
<div class="CalculatorInstance">
  <div class="calculator">
    <div class="display" id="values"> {{ numerador + " " + char + " " + denominador }}</div> 
    <div class="row">
      <td> <button @click="limparTudo" class="button">C</button></td>
      <td> <button @click="mudarSinal" class="button">+/-</button></td>
      <td> <button @click="porcentagem" class=" button">%</button></td>
      <td> <button @click="inserirOperador('/')" class="button">/</button></td>
      <td> <button @click="botaoOperadores" class="button font1">Operator</button></td>
    </div>     

    <div class="row">
      <td> <button @click="inserirNumero(1)" class="button">1</button></td>
      <td> <button @click="inserirNumero(2)" class="button">2</button></td>
      <td> <button @click="inserirNumero(3)" class="button">3</button></td>
      <td> <button @click="inserirOperador('x')" class="button">x</button></td>
    </div>


    <div class="row">
      <td> <button @click="inserirNumero(4)" class="button">4</button></td>
      <td> <button @click="inserirNumero(5)" class="button">5</button></td>
      <td> <button @click="inserirNumero(6)" class="button">6</button></td>
      <td> <button @click="inserirOperador('+')" class="button">+</button></td>
    </div>

    <div class="row">
      <td> <button @click="inserirNumero(7)" class="button">7</button></td>
      <td> <button @click="inserirNumero(8)" class="button">8</button></td>
      <td> <button @click="inserirNumero(9)" class="button">9</button></td>
      <td> <button @click="inserirOperador('-')" class="button">-</button></td>
    </div>

    <div class="row">
      <td> <button @click="decimal" class="button">.</button></td>
      <td> <button @click="inserirNumero(0)" class="button">0</button></td>
      <td> <button @click="calcular" class="button">=</button></td>
    </div>    
  </div>

  
  <div v-show="operatorTab" class="calculator op" >
    <div class="operator selection" colspan="2">
      <div>
        <input @click="selectionOperatorMethor(1)" type="radio" id="Log10" value="log10" name="operators" class="inputOption abaixo"/>
        <label for="log10" class="inputOption">Log<sub>10</sub> x</label><br><br>
      </div>
      <div>
        <input @click="selectionOperatorMethor(2)" type="radio" id="Logy x" value="logy x" name="operators" class="inputOption abaixo"/>
        <label for="logy x " class="inputOption">Log<sub>y</sub> x</label><br><br>
      </div>
      <div>
        <input @click="selectionOperatorMethor(3)" type="radio" id="x2" value="x2" name="operators" class="inputOption acima"/>
        <label for="x2" class="inputOption">x<sup>2</sup></label><br><br>
      </div>
      <div>
        <input @click="selectionOperatorMethor(4)" type="radio" id="xy" value="xy" name="operators" class="inputOption acima"/>
        <label for="xy" class="inputOption">x<sup>y</sup></label><br><br>
      </div>
      <div>
        <input @click="selectionOperatorMethor(5)" type="radio" id="sqrt" value="sqrt" name="operators" class="inputOption acima"/>
        <label for="sqrt" class="inputOption">√x</label><br><br>
      </div>
      <div>
        <input @click="selectionOperatorMethor(6)" type="radio" id="xy" value="xy" name="operators" class="inputOption acima"/>
        <label for="xy" class="inputOption"><sup>y</sup>√x</label><br><br>
      </div>

    </div>
    <div class="operator screen">
      <div class="operator displayO">
          <p class="text" v-show="selectionOperator==1">log<sub>10</sub> ({{ value1 }})</p>
          <p class="text" v-show="selectionOperator==2">log<sub>({{ value2 }})</sub> ({{ value1 }})</p>
          <p class="text" v-show="selectionOperator==3">({{ value1 }})<sup>2</sup></p>
          <p class="text" v-show="selectionOperator==4">({{ value2 }})<sup>({{ value1 }})</sup></p>
          <p class="text" v-show="selectionOperator==5">√({{ value1 }})</p>
          <p class="text" v-show="selectionOperator==6">({{ value2 }})√({{ value1 }})</p>
      </div><br>

      <div class="operator buttons">
        <button id="resetar" @click="limparOperadores">Limpar</button>
        <button @click="trocaDeCursor = !trocaDeCursor">Proximo</button>
        <button @click="enviarOperador">Enviar</button>
      </div> 
    </div>
  </div>  
</div>


</template>

<script>

export default {
  name: 'CalculatorInstance',
  data(){
    return{
      numerador : "",
      denominador: "",
      char: "",
      verificador: 0,
      operatorTab: false,
      value1: "",
      value2: "",
      selectionOperator: 0,
      trocaDeCursor: true
    }
  },

  methods: {

    inserirNumero(string){

      if(this.selectionOperator==0){

       if(this.verificador == 0){
          if(string != "0" || this.numerador != ""){
            this.numerador = this.numerador + string
          }
        }else if(this.verificador == 1){
          if(string != "0" || this.denominador != ""){
            this.denominador = this.denominador + string
          }
        }

      }else if(this.selectionOperator==1 || this.selectionOperator==3 || this.selectionOperator==5){
        
        if(string!="0"||this.value1 != ""){
          this.value1 = this.value1 + string
        }

      }else if(this.selectionOperator == 2 || this.selectionOperator == 4 || this.selectionOperator == 6){
        if(!this.trocaDeCursor){
          if(string!="0"||this.value1 != ""){
            this.value1 = this.value1 + string
          }
        }else{
          if(string!="0"||this.value2 != ""){
            this.value2 = this.value2 + string
          }
        }
      }
    },

    inserirOperador(operation){
      if(this.numerador != ""){
        this.char = operation
        this.verificador = 1
      }
    },

    calcular(){
      
      if(this.numerador != "" && this.denominador != ""){
        var number1 = Number(this.numerador)
        var number2 = Number(this.denominador)
        var fmtr = new Intl.NumberFormat('pt-br', {
          style: 'decimal',
          useGrouping: false,
          minimumFractionDigits: 2,
          maximumFractionDigits: 4
        });
        var result = 0

        if(this.char=="+"){
          result = (number1 + number2).toString()
          this.numerador = fmtr.format(result)

        }else if(this.char == "-"){
          result = (number1 - number2).toString()
          this.numerador = fmtr.format(result)

        }else if(this.char == "/"){
          result = (number1 / number2).toString()
          this.numerador = fmtr.format(result)

        }else if(this.char == "x"){
          result = (number1 * number2).toString()
          this.numerador = fmtr.format(result)
        }
        this.char = ""
        this.denominador = ""
        
      }

      this.verificador = 0
      this.numerador = this.numerador.replace(",",".")

    },

    limparTudo(){
      this.numerador = "",
      this.denominador = "",
      this.char = "",
      this.verificador = 0
    },

    mudarSinal(){
      if(this.numerador != "" && this.verificador == 0){
        this.numerador = (-(Number(this.numerador))).toString()
      }else if(this.denominador != "" && this.verificador ==1){
        this.denominador = (-(Number(this.denominador))).toString()
      }
    },

    porcentagem(){
      if(this.numerador!=""){
        var number1 = Number(this.numerador)
        var number2 = Number(this.denominador)

        if (this.char == ""){
          number1 = number1/100
          this.numerador = number1.toString()

        }else if (this.char == "/" || this.char == "x"){
          number2 = number2/100
          this.denominador = number2.toString()

        }else if (this.char == "+" || this.char == "-"){
          var porcentage = number1 * (number2/100)
          this.denominador = porcentage

        }
      }
        
    },

    decimal(){
      var check = 0
      if(this.char == ""){
          for (let index = 0; index < this.numerador.length; index++) {
            if(this.numerador.charAt(index) == "."){
              check = 1
              break
            }
          }
          if(check == 0){
            this.numerador = this.numerador + "."
          }

        
      }else{
        for (let index = 0; index < this.denominador.length; index++) {
          if(this.denominador.charAt(index) == "."){
            check = 1
            break
          }
        }
        if(check == 0){
          this.denominador = this.denominador + "."
        }
      }
    },

    botaoOperadores(){
      this.operatorTab = !this.operatorTab
      this.limparOperadores()

    },

    limparOperadores(){
      this.selectionOperator = 0
      var itens = document.getElementsByName("operators")
      for (let index = 0; index < itens.length; index++) {
        itens.item(index).checked = false
      }
      this.trocaDeCursor = true
      this.value1 = ""
      this.value2 = ""
      
    },

    enviarOperador(){
      var resultado = ""
      
      if(this.selectionOperator == 1 && this.value1 != ""){
        resultado = Math.log10(Number(this.value1)).toString()

      }else if (this.selectionOperator == 2 && this.value1 != "" && this.value2 != ""){
        resultado = (Math.log10(Number(this.value1))/Math.log10(Number(this.value2))).toString()

      }else if (this.selectionOperator == 3 && this.value1 != ""){
        resultado = Math.pow(this.value1,2).toString()

      }else if(this.selectionOperator == 4 && this.value1 != "" && this.value2 != ""){
        resultado = Math.pow(this.value2,this.value1).toString()

      }else if(this.selectionOperator == 5 && this.value1 != ""){
        resultado = Math.sqrt(this.value1,2).toString()

      }else if(this.selectionOperator == 6 && this.value1 != "" && this.value2 != ""){
        resultado = Math.pow(this.value1,1/this.value2)
      
      }

      if(this.char == ""){
        this.numerador = resultado
      }else if(this.char != ""){
        this.denominador = resultado
      }

      this.limparOperadores()

    },

    selectionOperatorMethor(id){
      this.selectionOperator = id
      this.value1=""
      this.value2=""
    }


  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.CalculatorInstance{
  margin-top: 10%;
  margin-left: 20%;
}


.calculator {
  float: left;
  margin-right: 10px;
  font-family: "Lucida Console", "Courier New", monospace;

}

.operator{
  float: left;
}

.operator > button{
  float: left;
  border-radius: 20px;
  width: 100px;
  margin-left: 5px;
  margin-top: 5px;
}

.line{
  height: 22px;
  min-height: 22px;
  
}

.selection{
  float: left;
  min-width: 100px ;
  vertical-align: 50%;

}
.acima{
  font-size: smaller;
}

.abaixo{
  font-size: smaller;
}

.inputOption{
  float: left;
}

.display{
  background-color: #333;
  color: white;
  width: 70%;
  height: 40px;
  font-size: 30px;
  table-layout:fixed;
  word-wrap:break-word;  
  position: initial;
  border-radius: 10px;

}


.displayO{
  border: 1px solid black;
  width: 315px;
  height: 100px;
  font-size: 20px;
}

.button{
  font-size: 30px;
  width: 90px;
  height: 90px;
  background-color: #f2f2f2;
  border: 1px solid #999;
  border-radius: 10px;
  font-family: "Lucida Console", "Courier New", monospace;
  

}
.op{
  margin-top: 50px;
  background-color: white;
}
.font1{
  width: 160px;
  

}






</style>
