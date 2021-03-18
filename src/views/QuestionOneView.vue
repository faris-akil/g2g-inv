<template>
  <div>
    <h3>A simple page to allow user enter message and auto convert the message to lowercase</h3>
    <v-row>
      <v-col cols="6" offset="3">
        <v-text-field label="Enter the text here" v-model="text"></v-text-field>
        <v-btn class="my-2" @click="convertText">Convert</v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6" offset="3">
        <div>
        Live Conversion: {{toLowerCase}}
        </div>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6" offset="3">
        <div>
        Via Button: {{convertedText}}
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
    // filters: {
    //     smallLetter(val){
    //         return val ? val.toLowerCase() : ''
    //     }
    // },
    computed: {
      toLowerCase(){
        return this.text.toLowerCase()
      }
    },
    data(){
        return {
            text: '',
            convertedText: ''
        }
    },
    methods: {
        convertText(){
            this.convertedText = this.text.toLowerCase()
        }
    }
};
</script>

<style>
</style>