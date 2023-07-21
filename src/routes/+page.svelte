<script>
  import Box from './Box.svelte';

let query = "";
let waitingOnResponse = false;
let responseText = "";
let q = "";



async function sendRequest() {
  q = query

  const url = "http://localhost:8080"; // Replace with your server URL
  const payload = { query }; 

  waitingOnResponse = true 
  try {
    const response = await fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(payload),
    });

    

    if (response.ok) {
      const data = await response.json();
      responseText = data.result;
      waitingOnResponse = false
    } else {
      responseText = "Error: " + response.status;
    }
  } catch (error) {
    responseText = "Error: " + error.message;
  }

  query = ""
  
}


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

.radios-container {
  flex-direction: column;
  align-items: flex-start; /* Align items to the start of the container */
  justify-content: flex-end; /* Align items to the bottom of the container */
}

.pad {
  padding-bottom: 10px;
}



@media (max-width: 767px) {
  /* Styles for screens up to 767px wide (typically mobile screens) */
  .container {
    width: 90%;
  }
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
<Box>
  <p>This App uses AI models which may produce inaccurate answers that could be unfactual or harmful. It is limited to only answer questions about gardening or related topics</p>
</Box>


<div class="features">Your gardening assistant</div>

{#if !responseText}
  <h3>I answer all gardening questions</h3>

  <div class="input-container">
    <textarea class="input" type="text" bind:value={query} on:input={query}></textarea>
    <button class="button" on:click={sendRequest}>Send</button>
  </div>
{/if}

{#if waitingOnResponse}
  <p>Waiting for response</p>
{/if}

    </div>

  </div>
</main>