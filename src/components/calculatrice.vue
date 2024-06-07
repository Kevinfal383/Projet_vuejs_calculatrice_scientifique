<template>
  <h1>CALCULATRICE 🤔🤓</h1>
  <div class="corps">
    <div class="calcul">
      <p>{{ calcul }}</p>
    </div>
    <div class="clavier">
      <div class="boutton">
        <button @click="ajouterOperateur('(')" class="bgGris">(</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur(')')" class="bgGris">)</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('^')" class="bgGris">^</button>
      </div>
      <div class="boutton">
        <button @click="supprimerTous()" class="bgGrisFaible">C</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('/')" class="bgGrisFaible">/</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('*')" class="bgGrisFaible">×</button>
      </div>
      <div class="boutton">
        <button @click="supprimer()" class="bgGrisFaible">DEL</button>
      </div>
      <div class="boutton">
        <button @click="ajouterFonction('factorial')" class="bgGris">x!</button>
      </div>
      <div class="boutton">
        <button @click="ajouterFonction('sqrt')" class="bgGris">√</button>
      </div>
      <div class="boutton">
        <button @click="ajouterFonction('nRoot')" class="bgGris">n√x</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(7)">7</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(8)">8</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(9)">9</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('-')" class="bgGrisFaible">-</button>
      </div>
      <div class="boutton">
        <button @click="ajouterFonction('exp')" class="bgGris">e</button>
      </div>
      <div class="boutton">
        <button @click="ajouterLn()" class="bgGris">ln</button>
      </div>
      <div class="boutton">
        <button @click="ajouterFonction('log')" class="bgGris">log</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(4)">4</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(5)">5</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(6)">6</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('+')" class="bgGrisFaible">+</button>
      </div>
      <div class="boutton">
        <button @click="ajouterFonction('sin')" class="bgGris">sin</button>
      </div>
      <div class="boutton">
        <button @click="ajouterFonction('cos')" class="bgGris">cos</button>
      </div>
      <div class="boutton">
        <button @click="ajouterFonction('tan')" class="bgGris">tan</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(1)">1</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(2)">2</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre(3)">3</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('=')" class="egale">=</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('^2')" class="bgGris">x²</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('^3')" class="bgGris">x³</button>
      </div>
      <div class="boutton">
        <button @click="ajouterPi()" class="bgGris">π</button>
      </div>
      <div class="boutton">
        <button @click="ajouterOperateur('%')">%</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre('0')">0</button>
      </div>
      <div class="boutton">
        <button @click="ajouterNombre('.')">.</button>
      </div>
    </div>
  </div>
</template>

<script>
import { evaluate } from 'mathjs';

export default {
  name: 'calculatriceVuejs',
  data() {
    return {
      calcul: "0",
    }
  },
  methods: {
    ajouterNombre(n) {
      if (this.calcul === "0") {
        this.calcul = String(n);
      } else {
        this.calcul = this.calcul + String(n);
      }
    },
    ajouterOperateur(op) {
      if (op === '=') {
        this.evaluerExpression();
      }
      // else if (op === '^') {
      //   this.calcul = this.calcul + '**';
      // } 
      else {
        this.calcul = this.calcul + op;
      }
    },
   evaluerExpression() {
      try {
        let expression = this.pretraiterExpression(this.calcul);
        this.calcul = String(evaluate(expression));
      } catch (e) {
        this.calcul = "Syntaxe erreur";
      }
    },
    supprimer() {
      if (this.calcul.length > 1) {
        this.calcul = this.calcul.slice(0, -1).trim();
      } else {
        this.calcul = "0";
      }
    },
    supprimerTous() {
      this.calcul = "0";
    },
    ajouterFonction(fn) {
      if (this.calcul === "0") {
        this.calcul = fn + '(';
      } else if ( fn === 'sqrt') {
        this.calcul = this.calcul + 'sqrt(';
      } else if (fn === 'nRoot') {
        this.calcul = this.calcul + 'nthRoot(';
      } else if (fn === 'sin' || fn === 'cos' || fn === 'tan' || fn === 'log') {
        this.calcul = this.calcul + fn + '(';
      } else if (fn === 'exp') {
        this.calcul = this.calcul + 'exp(';
      } else if (fn === 'pi') {
        this.calcul = this.calcul + 'pi';
      } else if (fn === 'factorial') {
        this.calcul = this.calcul + '!';
      } 
    },
    ajouterPi(){
      if (this.calcul === "0") {
        this.calcul = 'pi';
      } else {
        this.calcul = this.calcul + 'pi';
      }
    },
    ajouterLn() {
      if (this.calcul === "0") {
        this.calcul = 'ln(';
      } else {
        this.calcul = this.calcul + 'ln(';
      }
    },
    pretraiterExpression(expression) {
      return expression.replace(/ln/g, 'log');
    }
    
    
  }
}
</script>

<style lang="scss">
body {
  font-family: sans-serif;
  background: #000;
  color: white;
  h1 {
    font-size: 35px;
    text-align: center;
  }
  .calcul {
    border: 5px solid white;
    width: 840px;
    margin: 20px auto 0px;
    height: 100px;
    p {
      font-size: 40px;
      padding-left: 8px;
    }
  }
  .clavier {
    border: 5px solid white;
    margin: 0px auto;
    display: grid;
    grid-template: repeat(5, 70px) / repeat(7, 120px);
    width: 840px;
    button {
      background: #000;
      border: 2px solid white;
      color: white;
      font-size: 30px;
      text-align: center;
      width: 120px;
      height: 70px;
      &:hover{
        cursor: pointer;
        background: #2c2c2c;
      }
    }
    .egale{
      height: 140px;
      background: rgb(192, 192, 31);
      font-size: 50px;
      font-weight: bold;
      &:hover{
        background: rgb(231, 231, 46);
      }
    }
    .bgGris{
      background: #3f3f3f;
      &:hover{
        background: #5e5e5e;
      }
    }
    .bgGrisFaible{
      background: #8d8d8d;
      &:hover{
        background: #aaaaaa;
      }
    }
  }
}
</style>