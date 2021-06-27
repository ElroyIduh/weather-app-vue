<template>
  <div class="quote">
      <h2>{{ text }}</h2>
      <h3>{{ author }}</h3>
  </div> 
</template>

<script>
export default {
    props: ["text", "author"],
    data() {
      return{
        quote: null,
      }
    },
    created() {
      this.getDailyQuote()

    },
    methods: {
      getDailyQuote() {
        const url = "https://quotes.rest/qod"

        fetch(url)
        .then(response => {
          console.log(response)
        })
      }
    }
}
</script>

<style>
  .quote {
    color:hsl(0, 0%, 40%);
    font-style: italic;
  }

  .quote .text {
    font-size: 1,5rem;
  }

  .quote .text {
    font-size: 0,9rem;
  }
</style>