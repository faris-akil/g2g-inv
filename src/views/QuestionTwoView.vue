<template>
  <div class="ma-auto">
    <v-sheet outlined rounded color="blue darken-3" class="pa-2 mx-3">
      <v-row>
        <v-col cols="10" offset="1" class="white--text">
          <div class="d-flex">
            <v-col cols="3">
              <v-text-field
                dark
                outlined
                label="Amount"
                v-model="form.amount"
              />
            </v-col>
            <v-col cols="3">
              <v-select
                dark
                outlined
                label="From"
                v-model="form.from"
                :items="currency"
              />
            </v-col>
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
            <v-col cols="3" class="ma-auto">
              <v-select
                dark
                outlined
                label="To"
                v-model="form.to"
                :items="currency"
              />
            </v-col>
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
          <p class="subtitle-1">{{ form.amount }} {{ form.from }} =</p>
          <p class="display-2">{{ result }} {{ form.to }}</p>
          <p class="subtitle-2">1 {{ form.to }} = {{ reverseResult }}</p>
          <p class="subtitle-2">1 {{ form.from }} = {{ answer.toFixed(4) }} {{form.to}}</p>
        </div>
      </v-row>
    </v-sheet>
  </div>
</template>

<script>
import axios from "axios";

export default {
  watch: {
    form: {
      handler() {
        this.answer = "";
      },
      deep: true,
    },
  },
  computed: {
    result() {
      return this.answer * this.form.amount;
    },
    reverseResult() {
      return (1 / this.answer).toFixed(4) + " " + this.form.from;
    },
  },
  data() {
    return {
      form: {
        amount: "",
        from: "MYR",
        to: "USD",
      },
      currency: ["USD", "MYR", "EUR"],
      answer: "",
    };
  },
  methods: {
    async convertCurrency() {
      // This will be put at local environment but for this only test it will be put here
      let apiKey = "bdd63d7f3991b76bf8a4";
      let url = `https://free.currconv.com/api/v7/convert?q=${this.form.from}_${this.form.to}&compact=ultra&apiKey=${apiKey}`;
      try {
        let req = await axios.get(url);
        let result = req.data;
        let keys = Object.keys(result);
        this.answer = result[keys[0]];
      } catch (error) {
        alert(error, ', Please Try Again')
      }
    },
  },
};
</script>

<style>
</style>