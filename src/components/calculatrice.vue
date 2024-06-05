<template>
   <h1>CALCULATRICE 🤔🤓</h1>
    <div class="corps">
      <div class="calcul">
        <p>{{ calcul }}</p>
      </div>
      <div class="clavier">
        <div class="boutton">
          <button>(</button>
        </div>
        <div class="boutton">
          <button>)</button>
        </div>
        <div class="boutton">
          <button>^</button>
        </div>
        <div class="boutton">
          <button @click="supprimerTous()">C</button>
        </div>
        <div class="boutton">
          <button>/</button>
        </div>
        <div class="boutton">
          <button @click="ajouterOperateur('*')">×</button>
        </div>
        <div class="boutton">
          <button @click="supprimer()">DEL</button>
        </div>
        <div class="boutton">
          <button>x!</button>
        </div>
        <div class="boutton">
          <button>√</button>
        </div>
        <div class="boutton">
          <button>x√y</button>
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
          <button @click="ajouterOperateur('-')">-</button>
        </div>
        <div class="boutton">
          <button>e</button>
        </div>
        <div class="boutton">
          <button>ln</button>
        </div>
        <div class="boutton">
          <button>log</button>
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
          <button @click="ajouterOperateur('+')">+</button>
        </div>
        <div class="boutton">
          <button>sin</button>
        </div>
        <div class="boutton">
          <button>cos</button>
        </div>
        <div class="boutton">
          <button>tan</button>
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
          <button @click="ajouterOperateur('=')">=</button>
        </div>
        <div class="boutton">
          <button>x²</button>
        </div>
        <div class="boutton">
          <button>x³</button>
        </div>
        <div class="boutton">
          <button>Pi</button>
        </div>
        <div class="boutton">
          <button>%</button>
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
    export default {
      name: 'calculatriceVuejs',
      data(){
        return{
          calcul: "0",
        }
      },
      methods:{
        ajouterNombre(n){
          if (this.calcul === "0"){
            this.calcul = String(n)
          } else {
            this.calcul = this.calcul + String(n)
          }
        },
        ajouterOperateur(op){
          if (op === '='){
            this.evaluerExpession();
          } 
          else {
            this.calcul = this.calcul + op;
          }
        },
        /*evaluerExpession(){
          try {
          // Utilisation de Function constructor au lieu de eval() pour évaluer l'expression
          this.calcul = String(Function('"use strict";return (' + this.calcul + ')')());
        } catch (e) {
          this.calcul = "Erreur";
        }
        }*/
        //La fonction eval en JavaScript évalue une chaîne de caractères comme du code JavaScript et retourne le résultat de cette évaluation
        evaluerExpession(){
          try {
            this.calcul = String(eval(this.calcul));
          } catch (e) {
            this.calcul = "Syntaxe erreur";
          }
        },
        supprimer(){
          if (this.calcul.length > 1) {
            this.calcul = this.calcul.slice(0, -1).trim();
          } else {
            this.calcul = "0";
          }
        },
        supprimerTous(){
          this.calcul = "0";
        }
      }
    }
</script>
  
  
  <style lang="scss">
    body{
      font-family: sans-serif;
      background: #000;
      color: white;
      h1{
        font-size: 35px;
        text-align: center;
      }
      .calcul{
        border: 5px solid white;
        width: 840px;
        margin: 20px auto 0px;
        height: 100px;
        p{
          font-size: 40px;
          padding-left: 8px;
        }
      }
      .clavier{
        border: 5px solid white;
        margin: 0px auto;
        display: grid;
        grid-template: repeat(5, 80px) / repeat(7, 120px);
        width: 840px;
        button{
          background: #000;
          border: 2px solid white;
          color: white;
          font-size: 40px;
          text-align: center;
          width: 120px;
          height: 80px;
        }
      } 
    }
  </style>