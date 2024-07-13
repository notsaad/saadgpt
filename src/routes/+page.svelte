<script>
  import { onMount } from 'svelte';
  import { useChat } from '@ai-sdk/svelte';

  const { input, handleSubmit: originalHandleSubmit, messages } = useChat();
  let showSuggestions = true;

let suggestions = [
  { icon: '📈', text: 'What experience does Saad have?', value: 'What experience does Saad have?' },
  { icon: '📚', text: 'What is Saad studying?', value: 'What is Saad studying?' },
  { icon: '📫', text: 'Where can I contact Saad?', value: 'Where can I contact Saad?' },
  { icon: '🎮', text: "Where can I see Saad's projects?", value: "Where can I see Saad's projects?" }
];

const handleSubmit = () => {
  if ($input.trim() !== '') {
    showSuggestions = false;
    originalHandleSubmit();
  }
};

  const handleSuggestionClick = (suggestionValue) => {
  $input = suggestionValue;
  handleSubmit();
	};

</script>

<div class="page-content">
{#if showSuggestions}
  <div class="disappear">
    <div>
        <h3>try asking SaadGPT...</h3>
    </div>

	<div class="suggestions">
	{#each suggestions as suggestion}
		<button class="suggestion-button" on:click={() => handleSuggestionClick(suggestion.value)}>
		<span class="suggestion-icon">{suggestion.icon}</span>
		<span class="suggestion-text">{suggestion.text}</span>
		</button>
	{/each}
	</div>
  </div>
{/if}

  <main>
  <div class="messages-container">
      {#each $messages as message}
        <div class="message-wrapper {message.role === 'assistant' ? 'assistant' : 'user'}">
          <div class="message-bubble">
            {message.content}
          </div>
        </div>
      {/each}
    </div>


    <div class="input-area">
      <div class="input-wrapper">
        <input 
          type="text" 
          bind:value={$input} 
          placeholder="Ask SaadGPT about my projects, experience, etc..."
          on:keydown={(e) => e.key === 'Enter' && handleSubmit()}
        />
        <button class="send-button" on:click={handleSubmit}>
          <span class="icon">↑</span>
        </button>
      </div>
    </div>
    </main>

</div>

<style>

 .suggestions {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
    max-width: 600px;
    width: 100%;
  }
  h3{
	font-family: 'Roboto', sans-serif;
	font-weight: 900;
  }

  .suggestion-button {
    display: flex;
    align-items: center;
    padding: 12px;
    background-color: #3E3F4B;
    border: 1px solid #565869;
    border-radius: 8px;
    color: #fff;
    transition: background-color 0.3s ease;
	cursor: pointer;
  }

  .suggestion-button:hover{
	background-color: #50515f;
  }

  .suggestion-icon {
    margin-right: 10px;
    font-size: 1.2em;
  }

  .suggestion-text {
    font-size: 0.9em;
  }

  .disappear {
    position: relative;
    top: 70vh; 
    margin-bottom: 70vh;
  }

  @media (max-width: 600px) {
    .suggestions {
      grid-template-columns: 1fr;
    }
  }
  .page-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    padding: 20px;
  }

.messages-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  overflow-y: auto;
  height: calc(100vh - 150px);
}

.message-wrapper {
  display: flex;
  width: 100%;
}

.message-wrapper.assistant {
  justify-content: flex-start;
}

.message-wrapper.user {
  justify-content: flex-end;
}

.message-bubble {
	font-family: 'Roboto', sans-serif;
	font-weight: 400;
  max-width: 70%;
  padding: 10px 15px;
  border-radius: 20px;
  font-size: 14px;
  line-height: 1.4;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

.assistant .message-bubble {
  background-color: #f0f0f0;
  color: #333;
  border-bottom-left-radius: 5px;
}

.user .message-bubble {
  background-color: #e1f5fe;
  color: #333;
  border-bottom-right-radius: 5px;
}

main {
  font-family: 'SohneLight';
  display: flex;
  flex-direction: column;
  height: 100vh;
  padding-bottom: 80px; 
}

.input-area {
  position: fixed;
  bottom: 0;
  left: 120px;
  right: 0;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%; 
  z-index: 10; 
  pointer-events: none;
}

.input-wrapper {
  position: relative;
  max-width: 700px; 
  width: 60%; 
  margin: 0 auto;
  pointer-events: auto; 
}

input {
  width: 100%;
  padding: 10px 40px 10px 10px;
  background-color: #2F2F2F;
  border: 1px solid #565869;
  border-radius: 15px;
  color: #fff;
  box-sizing: border-box;
}

.send-button {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  padding: 5px 10px;
  background-color: #676767;
  border: none;
  border-radius: 15px;
  color: #fff;
  cursor: pointer;
  text-align: center;
}

.send-button:hover{
	color: #2F2F2F;
}

.send-button .icon {
  margin: 0; 
}
</style>