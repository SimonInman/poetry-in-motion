<script>
  import { flip } from "svelte/animate";
  import { dndzone } from "svelte-dnd-action";
  export let items;

  items = items.filter((line) => line.name != "\n");

  let correctlyPlacedSet = new Set();

  const flipDurationMs = 300;

  function handleDndConsider(e) {
    items = e.detail.items;
  }

  function handleDndFinalize(e) {
    items = e.detail.items;
  }
</script>

<div
  class="bank-border"
  use:dndzone={{ items, flipDurationMs }}
  on:consider={handleDndConsider}
  on:finalize={handleDndFinalize}
>
  {#each items as item (item.id)}
    <div class="blah" animate:flip={{ duration: flipDurationMs }}>
      <div class="line" class:correct={correctlyPlacedSet.has(item.id)}>
        {item.name}
      </div>
    </div>
  {/each}
</div>

<style>
  div.bank-border {
    width: 500px;
    padding: 0.3em;
    border: 1px solid black;
    box-sizing: border-box;
  }
  .correct {
    background-color: lightgreen;
  }

  div.line {
    padding-left: 5px;
    background-color: aliceblue;
  }

  div.blah {
    text-align: left;
    width: 100%;
    border: 0.8px solid blue;
    margin: 0.15em 0;
  }
</style>
