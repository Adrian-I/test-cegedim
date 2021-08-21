<template>
  <section class="testApp">
    <UserInput @new-input="setInput"/>
    <MaxValuesFromRange :numbersToProcess="numbersToProcess" @new-max-values="setMaxValues"/>
    <ValuesToChars :values="maxValues" @new-chars="setChars"/>
    <Matrix :values="chars"/>
 </section>
</template>

<script>

import UserInput from "@/components/UserInput";
import MaxValuesFromRange from "@/components/MaxValuesFromRange";
import ValuesToChars from "@/components/ValuesToChars";
import Matrix from "@/components/Matrix";


export default {
  name: 'App',
  components: {
    UserInput,
    MaxValuesFromRange,
    ValuesToChars,
    Matrix
  },

  data() {
    return {
      numbersToProcess:[],
      maxValues:[],
      chars:[]
    }
  },
  methods: {
    setInput( input ) {
      this.numbersToProcess = input;
    },

    setMaxValues( values) {
      this.maxValues = values;
    },

    setChars(values) {
      this.chars = values;
    }
  }
}
</script>

<style scoped>
.testApp {
  padding: 100px 30px;
  max-width: 700px;
  margin: 0 auto;
}
</style >
