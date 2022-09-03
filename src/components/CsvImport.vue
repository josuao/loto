<template>
<div>
    <select v-model="jour">
      <option>SAMEDI</option>
      <option>LUNDI</option>
      <option>MERCREDI</option>
    </select>

     <button @click="AjoutAuTableau">Afficher</button>
   <!--  <div v-for="jour in lotoJson" v-bind:key="jour.index">
      <div v-if="jour.jour_de_tirage === 'SAMEDI'">
         {{jour.combinaison_gagnante_en_ordre_croissant}}
      </div>
        <div v-else><p>Pas samedi</p></div>
    </div> -->
    <div class="grid title">
      <div>
        Numero
      </div>
      <div @click="ChangeOrder()">
        Nombre de sortie pour {{tableauTirage.length}} tirages
      </div>
      <div @click="ChangeOrder()">
        Pourcentage gagnant
      </div>
    </div>
    <div class="grid" v-for="ligne in tableauOccurence" v-bind:key="ligne.index">
      <div>
        {{ligne.numero}}
      </div>
      <div>
        {{ligne.occurence}} 
      </div>
      <div>
        {{((ligne.occurence / lotoJson.length) * 100).toFixed(2)}} %
      </div>
    </div>
    <h2>Numero chance</h2>
    <div class="grid title">
      <div>
        Numero
      </div>
      <div @click="ChangeOrder()">
        Nombre de sortie
      </div>
      <div @click="ChangeOrder()">
        Pourcentage gagnant
      </div>
    </div>
    <div class="grid" v-for="ligne in tableauOccurenceNumeroChance" v-bind:key="ligne.index">
      <div>
        {{ligne.numero}}
      </div>
      <div>
        {{ligne.occurence}}
      </div>
      <div>
        {{((ligne.occurence / lotoJson.length) * 100).toFixed(2)}} %
      </div>
    </div>
    <h2>Tirage</h2>
    <div class="grid title">
      <div>
        Tirage
      </div>
      <div @click="ChangeOrder()">
        Nombre de sortie
      </div>
      <div @click="ChangeOrder()">
        Pourcentage gagnant
      </div>
    </div>
    <div class="grid" v-for="ligne in tableauOccurenceTirage" v-bind:key="ligne.index">
      <div>
        {{ligne.numero}}
      </div>
      <div>
        {{ligne.occurence}}
      </div>
      <div>
        {{(ligne.occurence / lotoJson.length) * 100}} %
      </div>
    </div>
    
    
</div>
   
    
</template>
<script>
import json from '../assets/csvjson.json'
export default {
  name: "CsvImport",
  data() {
    return {
      lotoJson: json,
      jour: 'SAMEDI',
      tableauResult : [],
      tableauOccurence : [],
      tableauNumeroChance : [],
      tableauOccurenceNumeroChance: [],
      tableauTirage: [],
      tableauOccurenceTirage: [],
      i: 0,
      j: 1,
      h: 0,
      ordreDirection: 'normal'
    };
  },
  methods:{
    AjoutAuTableau() {
      for(this.i = 0; this.i < this.lotoJson.length; this.i ++){
        if(this.lotoJson[this.i].jour_de_tirage === this.jour){
          this.tableauResult.push(this.lotoJson[this.i].boule_1, this.lotoJson[this.i].boule_2, this.lotoJson[this.i].boule_3, this.lotoJson[this.i].boule_4, this.lotoJson[this.i].boule_5)
          this.tableauNumeroChance.push(this.lotoJson[this.i].numero_chance)
          this.tableauTirage.push(this.lotoJson[this.i].combinaison_gagnante_en_ordre_croissant)
        }
          
      }
      for(this.j = 0; this.j < 49; this.j++){
        let taboccu = this.tableauResult.filter(element => element == this.j + 1)
        this.tableauOccurence.push({numero : this.j + 1, occurence : taboccu.length })
      }
      for(this.h = 0; this.h < 10; this.h++){
        let taboccu = this.tableauNumeroChance.filter(element => element == this.h + 1)
        this.tableauOccurenceNumeroChance.push({numero : this.h + 1, occurence : taboccu.length })
      }
      for(let k = 0; k < this.tableauTirage.length; k++){
        let taboccu = this.tableauTirage.filter(element => element == k + 1)
        console.log(taboccu)
        this.tableauOccurenceTirage.push({numero : this.tableauTirage[k], occurence : taboccu.length })
      }

    },
    ChangeOrder() {
     
        if(this.ordreDirection ==='normal' || this.ordreDirection === "down"){
          this.ordreDirection = "up"
          this.tableauOccurence.sort(function(a, b) {
            return b.occurence - a.occurence
          });
           this.tableauOccurenceNumeroChance.sort(function(a, b) {
            return b.occurence - a.occurence
          });
        }else{
          this.ordreDirection = "down"
          this.tableauOccurence.sort(function(a, b) {
            return a.occurence - b.occurence
          });
          this.tableauOccurenceNumeroChance.sort(function(a, b) {
            return a.occurence - b.occurence
          });
        }     
    }
  }
  
};
</script>
<style lang="scss" scoped>
  .grid{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    row-gap: 20px;
    column-gap: 20px;
    div{
       
    }
  }
</style>