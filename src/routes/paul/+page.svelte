<script>
    import { onMount } from 'svelte';
    import Column from './Column.svelte';
    import Button from '@smui/button';
  
    let numberOfColumns = 5;
    let columns = [];
    let columnsPerPage = 5;
    let columnGap = '10';
  
    function initializeColumns() {
      columns = Array(numberOfColumns).fill().map((_, i) => ({
        title: `Column ${i + 1}`,
        rows: Array(Math.floor(Math.random() * 4) + 1).fill().map((_, j) => ({
          title: `Row ${j + 1}`,
          description: `Description ${j + 1}`,
        }))
      }));
    }
  
    function updateNumberOfColumns() {
      if (numberOfColumns < columns.length) {
        columns = columns.slice(0, numberOfColumns);
      } else {
        while (columns.length < numberOfColumns) {
          columns.push({ title: `Column ${columns.length + 1}`, rows: [] });
        }
      }
    }
  
    onMount(initializeColumns);
  </script>
  
  <svelte:head>
    <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />
    <link href="https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400;700&display=swap" rel="stylesheet">
  </svelte:head>
  
  <main>
    <h1>Columns and Rows</h1>
    <div class="control-panel">
      <label for="columnCount">Number of Columns:</label>
      <input type="number" id="columnCount" bind:value={numberOfColumns} min="1" on:change={updateNumberOfColumns}>
      <label for="columnsPerPage">Columns Per Page:</label>
      <input type="number" id="columnsPerPage" bind:value={columnsPerPage} min="1" max="10">
      <label for="columnGap">Column Gap (px):</label>
      <input type="number" id="columnGap" bind:value={columnGap} min="0" max="50">
      <Button on:click={updateNumberOfColumns} variant="raised">Update</Button>
    </div>
    <div class="columns-container">
      <div class="columns" style="--columns-per-page: {columnsPerPage}; --column-gap: {columnGap}px;">
        {#each columns as column, columnIndex}
          <Column {column} {columnIndex} bind:columns />
        {/each}
      </div>
    </div>
  </main>
  
  <style>
    :global(body) {
      background-color: #f0f0f0;
      font-family: 'Roboto Mono', monospace;
      margin: 0;
      padding: 0;
    }
  
    main {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 100%;
      padding: 2rem 0;
    }
  
    h1 {
      color: #1976d2;
      text-align: center;
    }
  
    .control-panel {
      margin-bottom: 2rem;
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 1rem;
      flex-wrap: wrap;
    }
  
    .control-panel input {
      width: 60px;
      padding: 0.5rem;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
  
    .columns-container {
      width: 100%;
      display: flex;
      justify-content: center;
    }
  
    .columns {
      display: grid;
      grid-template-columns: repeat(var(--columns-per-page), minmax(250px, 1fr));
      gap: var(--column-gap);
      max-width: calc((250px * var(--columns-per-page)) + (var(--column-gap) * (var(--columns-per-page) - 1)));
    }
  </style>