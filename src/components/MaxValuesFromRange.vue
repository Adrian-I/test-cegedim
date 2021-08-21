<template>
  <p>Maximele din clase: <span v-if="maxValues.length">{{ maxValues }}</span></p>

</template>

<script>

export default {
  name: 'MaxValuesFromRange',
  props: {
    numbersToProcess: Array,
  },

  data() {
    return {
      maxValues:[],
    }

  },

  watch: {
    numbersToProcess: function () {
      this.maxValues = [];
      const ranges = [
        {
          min:100,
          max:200,
          maxValueFound: 0,
        },

        {
          min:200,
          max:300,
          maxValueFound: 0,
        },

        {
          min:300,
          max:400,
          maxValueFound: 0,
        },

        {
          min:400,
          max:500,
          maxValueFound: 0,
        },

        {
          min:500,
          max:600,
          maxValueFound: 0,
        },

        {
          min:600,
          max:700,
          maxValueFound: 0,
        },

        {
          min:700,
          max:800,
          maxValueFound: 0,
        },

        {
          min:800,
          max:900,
          maxValueFound: 0,
        },

        {
          min:900,
          max:1000,
          maxValueFound: 0,
        }
      ]

      this.numbersToProcess.forEach((number) => {
        ranges.forEach(range => {
          if ( number >= range.min && number < range.max && number > range.maxValueFound) {
            range.maxValueFound = number;
          }
        })
      })

      ranges.forEach(element => {
        if (element.maxValueFound !== 0 ) {
          this.maxValues.push(element.maxValueFound)
        }
      })

      this.$emit('new-max-values',this.maxValues)
    },
  },

}


</script>