<template>
  <form @submit="onSubmit" class="userInput">

    <label for="inputNumber">Introduceti un sir de numere intre 100 si 999 separate prin virgula:</label>

    <input type="text"
           v-model="numbers"
           id="inputNumber"
           name="text"
           placeholder="110, 120, 130, 280, 780, 510, 505, 605, 720, 230, 210, 275">

    <button type="submit">Calculate</button>
  </form>

  <p v-if="errors.length">
    <b>Erori de validare:</b>
    <ul>
      <li v-for="(error,index) in errors" :key="`error-${index}`">{{ error }}</li>
    </ul>
  </p>

</template>

<script>

export default {
  name: "UserInput",
  data() {
    return {
      numbers: "",
      errors: []
    }
  },



  methods: {
    onSubmit(e) {
      e.preventDefault();
      this.validateString()

      if (this.errors.length === 0) {
        this.$emit('new-input', this.numbers)
      }

    },

    validateString() {
      if ( typeof this.numbers !== "string" ) return;

      const inputString = this.numbers.split(',');
      this.errors = [];

      inputString.forEach(element => {

            if (isNaN(element) || element < 100 || element > 999) {
              this.errors.push(`${element} is invalid`);
            }
          }
      )

      if ( this.errors.length === 0 ) {
        this.numbers = inputString.map(element => element.trim())
      }
    }
  },
  emits: ['new-input']

}
</script>

<style scoped>

.userInput {
  display: flex;
  flex-wrap: wrap;
}

.userInput label {
  flex: 1 0 100%;
  font-size: 20px;
  padding-bottom: 10px;
}

.userInput input {
  flex: 1;
}

.userInput button {
  margin-left: 20px;
}

</style>