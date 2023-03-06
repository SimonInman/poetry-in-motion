<script>
  import { flip } from "svelte/animate";
  import { dndzone } from "svelte-dnd-action";
  export let items;
  export let slotIndex;

  let currentItemId;

  const flipDurationMs = 300;

  $: options = {
    dropFromOthersDisabled: items.length,
    items,
    flipDurationMs,
  };

  function handleDndConsider(e) {
    items = e.detail.items;
  }

  function handleDndFinalize(e) {
    items = e.detail.items;
    if (items.length > 0) {
      currentItemId = items[0].id;
    } else {
      currentItemId = null;
    }
  }
</script>

<div
  class="foo"
  use:dndzone={options}
  on:consider={handleDndConsider}
  on:finalize={handleDndFinalize}
  class:firstSlot={slotIndex === 0}
  class:correct={slotIndex === currentItemId}
>
  {#each items as item (item.id)}
    <div
      class="blah line"
      animate:flip={{ duration: flipDurationMs }}
      class:correct={slotIndex === item.id}
    >
      {#if item.name === "\n"}
        <!-- skip -->
      {:else}
        {item.name}
      {/if}
    </div>
  {/each}
</div>

<style>
  .foo {
    width: 500px;
    padding: 0.2em;
    border: 1px solid black;
    border-top: 0px;
    height: 16px;
  }
  .foo:nth-child(1) {
    border-top: 1px solid black;
  }
  .correct {
    background-color: lightgreen;
  }

  div.line {
    padding-left: 5px;
    line-height: 16px;
  }

  div.blah {
    text-align: left;
    width: 100%;
    border: 0px solid blue;
  }
</style>
