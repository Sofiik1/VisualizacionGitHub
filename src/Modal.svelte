<script>
  import { createEventDispatcher, onMount } from 'svelte';
  const dispatch = createEventDispatcher();

  function handleKeydown(event) {
    if (event.key === 'Escape') {
      dispatch('close');
    }
  }

  onMount(() => {
    window.addEventListener('keydown', handleKeydown);
    return () => {
      window.removeEventListener('keydown', handleKeydown);
    };
  });
</script>

<style>
  .modal-backdrop {
    position: fixed;
    inset: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 50;
  }

  .modal-content {
    background: rgb(2, 2, 2);
    border-radius: 1rem;
    padding: 1.5rem;
    max-width: 800px;
    max-height: 90vh;
    width: 90%;
    border: 2px solid rgba(0, 255, 200, 0.364); 
    position: relative;
  }


  .close-btn {
    position: absolute;
    top: 0.75rem;
    right: 1rem;
    font-size: 1.2rem;
    background: none;
    border: none;
    cursor: pointer;
    color: #666;
  }
</style>

<div class="modal-backdrop" on:click={() => dispatch('close')} role="presentation">
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <!-- svelte-ignore a11y-no-static-element-interactions -->
  <div class="modal-content" on:click|stopPropagation>
    <button class="close-btn" on:click={() => dispatch('close')}>×</button>
    <slot />
  </div>
</div>
