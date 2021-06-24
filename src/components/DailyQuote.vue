<template>
  <div class="text">
      <h1>Daily Quote</h1>
        <p>{{ text }}</p>
        
  </div>

  <div class="author">
      <h2><p>{{ author }}</p></h2>
  </div>
</template>

<script>
export default {
    props: ["text", "author"]

}
</script>

<style>

</style>