<script>
    import Row from './Row.svelte';
    import { onMount } from 'svelte';
  
    export let column;
    export let columnIndex;
    export let columns;
  
    let titleBackgroundColor;
  
    function addRow() {
      column.rows = [...column.rows, { 
        title: `New Row`, 
        description: "New Description",
        headerColor: getRandomColor()
      }];
      columns = columns;
    }
  
    function removeRow(rowIndex) {
      column.rows = column.rows.filter((_, i) => i !== rowIndex);
      columns = columns;
    }
  
    function getRandomColor() {
      return '#' + Math.floor(Math.random()*16777215).toString(16);
    }
  
    onMount(() => {
      titleBackgroundColor = getRandomColor();
    });
  </script>
  
  <div class="column">
    <h2 style="background-color: {titleBackgroundColor};">{column.title}</h2>
    <button class="add-row" on:click={addRow}>Add Row</button>
    {#each column.rows as row, rowIndex}
      <Row {row} on:remove={() => removeRow(rowIndex)} />
    {/each}
  </div>
  
  <style>
    .column {
      display: flex;
      flex-direction: column;
      align-items: stretch;
    }
  
    h2 {
      color: #ffffff;
      margin-top: 0;
      margin-bottom: 1.5rem;
      text-align: center;
      font-size: 1.8rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      padding: 0.5rem;
      border-radius: 4px;
    }
  
    .add-row {
      display: block;
      width: 100%;
      margin-bottom: 1rem;
      background-color: #ff9800;
      color: #1e1e1e;
      border: none;
      padding: 0.5rem 1rem;
      cursor: pointer;
      border-radius: 4px;
      font-weight: bold;
      transition: background-color 0.3s ease;
    }
  
    .add-row:hover {
      background-color: #ffa726;
    }
  </style>