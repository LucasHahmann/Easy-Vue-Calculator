<template>
    <v-app>
        <div id="Calcultator">
            <v-text-field disabled :value="calc"></v-text-field>
            <v-container>
                <v-row>
                    <v-col @click="addNumber('7')" class="button">
                        7
                    </v-col>
                    <v-col @click="addNumber('8')" class="button">
                        8
                    </v-col>
                    <v-col @click="addNumber('9')" class="button">
                        9
                    </v-col>
                    <v-col @click="addOperation('x')" class="button">
                        x
                    </v-col>
                </v-row>
                <v-row>
                    <v-col @click="addNumber('4')" class="button">
                        4
                    </v-col>
                    <v-col @click="addNumber('5')" class="button">
                        5
                    </v-col>
                    <v-col @click="addNumber('6')" class="button">
                        6
                    </v-col>
                    <v-col @click="addOperation('-')" class="button">
                        -
                    </v-col>
                </v-row>
                <v-row>
                    <v-col @click="addNumber('1')" class="button">
                        1
                    </v-col>
                    <v-col @click="addNumber('2')" class="button">
                        2
                    </v-col>
                    <v-col @click="addNumber('3')" class="button">
                        3
                    </v-col>
                    <v-col @click="addOperation('+')" class="button">
                        +
                    </v-col>
                </v-row>
                <v-row>
                    <v-col @click="addOperation('=')" class="button">
                        =
                    </v-col>
                    <v-col @click="addOperation('c')" class="button">
                        C
                    </v-col>
                </v-row>
            </v-container>
        </div>
    </v-app>
</template>

<script>
export default {
  created () {
  },
  data () {
    return {
        calc: "",
        NumberArray: []
    }
  },
  methods: {
    calculateFromString(fn) {
        return new Function('return ' + fn)();
    },
    calculate(array){
        var stringArray = array.join(' ')
        return this.calculateFromString(stringArray)
    },
    checkIfFirstElement(){
        if(this.NumberArray.length == 0) return true
        return false    
    },
      addNumber(number){
          this.calc += number
      },
      addOperation(operator){
          switch(operator){
                case "x":
                    if(this.checkIfFirstElement()){
                        this.NumberArray.push(this.calc)
                        this.NumberArray.push("*")
                    }else {
                        this.NumberArray.push(this.calc)
                        this.NumberArray.push("*")
                    }
                    this.calc = ""
                    break
                case "-":
                    if(this.checkIfFirstElement()){
                        this.NumberArray.push(this.calc)
                        this.NumberArray.push("-")
                    }else {
                        this.NumberArray.push(this.calc)
                        this.NumberArray.push("-")
                    }
                    this.calc = ""
                    break
                case "+":
                    if(this.checkIfFirstElement()){
                        this.NumberArray.push(this.calc)
                        this.NumberArray.push("+")
                    }else {
                        
                        this.NumberArray.push(this.calc)
                        this.NumberArray.push("+")
                    }
                    this.calc = ""
                    break
                case "=":
                    this.NumberArray.push(this.calc)
                    var sum = this.calculate(this.NumberArray)
                    this.calc = sum
                    this.NumberArray = [];
                    break
                case "c":
                    this.NumberArray = [];
                    this.calc = "";
                    break
          }
      }
  },
    
}
</script>

<style>
.button{
    border-style: solid;
    border-radius: 5px;
    margin: 10px;
    height: 50px;
}
</style>