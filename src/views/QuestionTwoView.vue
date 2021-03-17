<template>
  <div class="ma-auto">
    <v-sheet outlined rounded color="blue darken-3" class="pa-2 mx-3">
      <v-row>
        <v-col cols="10" offset="1" class="white--text">
          <div class="d-flex">
            <v-col cols="3"> <v-text-field dark outlined label="Amount" v-model="amount"/> </v-col>
            <v-col cols="3"> <v-select dark outlined label="From" v-model="from" :items="currency" /> </v-col>
            <v-col cols="1">
                <div class="flex-column">
                    <div>
                    <v-icon class="white--text">mdi-arrow-right</v-icon>
                    </div>
                    <div>
                    <v-icon class="white--text">mdi-arrow-left</v-icon>
                    </div>
                </div>
            </v-col>
            <v-col cols="3" class="ma-auto"> <v-select dark outlined label="To" v-model="to" :items="currency"/> </v-col>
            <v-col cols="2" class="my-2">
                <v-btn dark @click="convertCurrency" color="orange">
                    convert <v-icon>mdi-arrow-right</v-icon>
                </v-btn>
            </v-col>
          </div>
        </v-col>
      </v-row>
      <v-row v-if="answer">
          <div class="mx-auto white--text">
              <p class="subtitle-1">{{amount}} {{from}} =</p>
              <p class="display-2">{{answer * amount}} {{to}}</p>
          </div>
      </v-row>
    </v-sheet>
  </div>
</template>

<script>
import axios from 'axios'

export default {
    watch: {
        amount(){
            this.answer=""
        },
        from(){
            this.answer=""
        },
        to(){
            this.answer=""
        },
    },
    data(){
        return {
            currency: ["USD", "MYR", "EUR"],
            amount: "",
            from: "MYR",
            to: "USD",
            answer: ""
        }
    },
    methods: {
        async convertCurrency(){
            // This will be put at local environment but for this only test it will be put here 
            let apiKey = 'bdd63d7f3991b76bf8a4';
            let req = await axios.get(`https://free.currconv.com/api/v7/convert?q=${this.from}_${this.to}&compact=ultra&apiKey=${apiKey}`)
            let result = req.data
            let key
            for (let i in result){
                key = i
            }
            this.answer = result[key]
        }
    }
};
</script>

<style>
</style>