<template>
  <div class="card quote">
    <div>
      <h3>{{ text }}</h3>
      <h4>{{ author }}</h4>
    </div>
  </div>
</template>

<script>
export default {
  props: ["text", "author"],
  data() {
    return {
      quote: null,
    };
  },
  created() {
    this.getDailyQuote();
  },
  methods: {
    getDailyQuote() {
      const url = "https://quotes.rest/qod";

      fetch(url).then((response) => {
        console.log(response);
      });
    },
  },
};
</script>

<style>
.quote {
  color: hsl(0, 0%, 40%);
  font-style: italic;
  display: flex;
  justify-content: center;
  align-items: center;
}
/*
  element
  .class
  #id
  ::pseudo-class
*/

.quote div {
  padding: 2rem;
}

.quote .text {
  font-size: 1, 5rem;
}

.quote .text {
  font-size: 0, 9rem;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  width: 40%;
  border-radius: 5px;
}
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}
</style>