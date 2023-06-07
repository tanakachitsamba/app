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

.input-container {
display: flex;
flex-direction: column;
align-items: flex-start; /* Align items to the start of the container */
justify-content: flex-end; /* Align items to the bottom of the container */
}

.input {
width: 97%;
//width: auto;
border: 1px solid #ccc;
padding: 10px;
font-size: 20px;
resize: vertical;
min-height: 200px;
margin-bottom: 10px;
border-radius: 5px;

resize: none; /* Prevent manual resizing */
overflow: hidden; /* Hide scrollbars */
}

.button {
padding: 10px 20px;
font-size: 16px;
font-weight: bold;
text-align: center;
text-decoration: none;
text-transform: uppercase;
border-radius: 4px;
border: 2px solid rgba(76, 175, 80, 0.5);
color: #fff;
background-color: #4CAF50;
box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
transition: color 0.3s ease, background-color 0.3s ease;
cursor: pointer;
width: auto; /* Set width to auto to occupy only the necessary space */
align-self: flex-end; /* Align the button to the right within the container */
}

.button:hover {
background-color: #75ca79;
}

.button:active {
background-color: #3e8e41;
}

.button:focus {
outline: none;
}


.answer {
font-size: 20px;
}

.features {
font-weight: 600;
font-size: 32px;    
}

.container {
  width: 60%;
  margin: auto;
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

{#if responseText}
  <div>
    <h2>Question</h2>
    <p>{q}</p>
    <h2>Answer</h2>
    <p class="answer">{responseText}</p>
  </div>

  <div class="input-container">
    <textarea class="input input_" type="text" bind:value={query} on:input={query}></textarea>
    <button class="button" on:click={sendRequest}>Send</button>
  </div>
{/if}
</div>
</main>