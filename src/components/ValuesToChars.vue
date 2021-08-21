<template>
  <p>Modulo:<span v-if="valuesTransformed.length">{{ valuesTransformed }}</span></p>
</template>

<script>
export default {
  name:'ValuesToChars',

  props: {
    values:Array
  },

  data() {
    return {
      valuesTransformed:[]
    }
  },

  watch: {
    values() {
      this.valuesTransformed = [];

      this.values.forEach(element => {
        this.valuesTransformed.push( String.fromCharCode(element % 26 + 65))
      })

      this.$emit('new-chars', this.valuesTransformed)
    },


  }
}
</script>