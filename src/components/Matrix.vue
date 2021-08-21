<template>
  <ul class="matrix" v-if="valuesDisplayed.length">
    <li v-for="(value,index) in valuesDisplayed" 
        @click="showCharacter(index)" 
        :key="valuesDisplayed[index].char" 
        :class="[isNaN(valuesDisplayed[index].char)?'isHoverable':'']">
         {{valuesDisplayed[index].showedValue}}
    </li>
  </ul>
</template>

<script>
export default {
  name: "Matrix",
  props: {
    values: Array
  },

  data() {
    return {
      valuesDisplayed: [],
      
    }
  },

  watch: {
    values() {
      this.valuesDisplayed = []

      for ( let i = 0; i < 16 ; i++ ){
        this.valuesDisplayed.push(
            { "char" :this.values[i] || i,
              "showedValue": "?"
            }
        )
      }

     this.shuffle(this.valuesDisplayed)
    }
  },

  methods: {
    showCharacter(index) {

      if(isNaN(this.valuesDisplayed[index].char)) {
        this.valuesDisplayed[index].showedValue = this.valuesDisplayed[index].char;
      }
    },

    shuffle( array) {
      let first,
          second,
          temp,
          count = array.length;
      for (let i = 0; i < 10; i++) {
        first = Math.floor(Math.random() * count);
        second = Math.floor(Math.random() * count);
        temp = array[first];
        array[first] = array[second];
        array[second] = temp;
      }
    }
  }
}
</script>

<style scoped>
.matrix {
  display: flex;
  flex-wrap: wrap;
  border: 1px solid #5E9DD5;
  list-style-type: none;
  padding: 0;
  font-size: 0;
  box-sizing: border-box;
}

.matrix li {
  background: #F0FFFF;
  border: 3px solid #FAEBD7;
  font-size: 30px;
  font-weight: bold;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 25%;
  box-sizing: border-box;
  cursor: pointer;
  transition: .2s ease-in-out;
}

.matrix li:before {
  content: '';
  display: block;
  padding-bottom: 73%;
}

.matrix li.isHoverable:hover {
  background: #7FFFD4FF;
}
</style>