<script>

</script>

<style lang="postcss">
:global(html) {
  background-color: theme(colors.white);
  margin: 0; padding: 0; 
}

.container {
  width: 80%;
  margin: auto;
}

.nav_ {
  padding-top: 20px;
  padding-bottom: 20px;
  font-size: 25px;
  font-weight: 600;
  text-transform: uppercase;
}

.about {
 width: 80%;
 margin: auto;
 padding-top: 40px;
}

.col {
  display: grid;
  grid-template-columns: 1fr; /* Set the number of columns as needed */
  grid-gap: 10px; /* Adjust the gap between divs as desired */
}
</style>

<main>
  <div class="container">
    <div class="nav_">🌑</div>

<div class="container">
<div class="features">Your gardening assistant</div>
<Box>
  <p>This App uses AI models which may produce inaccurate answers that could be unfactual or harmful. It is limited to only answer questions about gardening or related topics</p>
</Box>

{#if !responseText}
  <h3>I answer all gardening questions</h3>

  <div class="input-container">
    {#if ifOptions}
    <div class="radios-container pad">
      <div class="pad">Models</div>
      <label>
          <input type="radio" bind:group={modelNum} value={1} />gbt-3.5 (fast) 
      </label>
  
      <label>
          <input type="radio" bind:group={modelNum} value={2} />gbt-4 (slow but smarter)
      </label>

      <label>
        <div>Maximum length</div>
        <input type="number" bind:value={a} min="200" max="3000" />
      </label>
      
    <div>
      Latest Work 
    </div>
    <div class="col">
      <div class="c">1</div>
      <div  class="c">2</div>
      <div  class="c">3</div>
    </div>

    </div>

  </div>
</main>