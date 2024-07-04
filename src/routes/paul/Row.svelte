<script>
    import { createEventDispatcher } from 'svelte';
  
    export let row;
    const dispatch = createEventDispatcher();
  
    function removeRow() {
      dispatch('remove');
    }
  </script>
  
  <div class="row">
    <div class="row-header" style="background-color: {row.headerColor};">
      <h3>{row.title}</h3>
      <button class="remove-row" on:click={removeRow}>X</button>
    </div>
    <input bind:value={row.title} placeholder="Row Title">
    <textarea bind:value={row.description} placeholder="Row Description"></textarea>
  </div>
  
  <style>
    .row {
      background-color: #333;
      margin-bottom: 1rem;
      border-radius: 4px;
      overflow: hidden;
    }
  
    .row-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.5rem;
    }
  
    h3 {
      color: white;
      margin: 0;
      font-size: 1rem;
    }
  
    input, textarea {
      display: block;
      width: 100%;
      background-color: #444;
      color: #e0e0e0;
      border: none;
      padding: 0.5rem;
      font-size: 0.9rem;
      font-family: inherit;
    }
  
    textarea {
      height: 5em;
      resize: vertical;
    }
  
    .remove-row {
      background-color: rgba(0, 0, 0, 0.3);
      color: white;
      border: none;
      padding: 0.25rem 0.5rem;
      cursor: pointer;
      border-radius: 4px;
      font-weight: bold;
      transition: background-color 0.3s ease;
    }
  
    .remove-row:hover {
      background-color: rgba(0, 0, 0, 0.5);
    }
  </style>