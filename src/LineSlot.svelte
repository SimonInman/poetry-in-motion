<script>
  import { flip } from "svelte/animate";
  import { dndzone } from "svelte-dnd-action";
  export let items;
  export let slotIndex;

  let currentItemId;

  //   let correctlyPlacedSet: Set<number>;
  let correctlyPlacedSet = new Set();

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
    }

    console.log(
      "is dropFromOthersDisabled: %s",
      options.dropFromOthersDisabled
    );
  }
</script>

<section
  use:dndzone={options}
  on:consider={handleDndConsider}
  on:finalize={handleDndFinalize}
  class:correct={slotIndex === currentItemId}
>
  {#each items as item (item.id)}
    <div class="blah" animate:flip={{ duration: flipDurationMs }}>
      {#if item.name === "\n"}
        <!-- skip -->
      {:else}
        <div class="line" class:correct={slotIndex === item.id}>
          {item.name}
        </div>
      {/if}
    </div>
  {/each}
</section>

<style>
  section {
    width: 100%;
    padding: 0.2em;
    border: 1px solid black;
    height: 16px;
  }
  .correct {
    background-color: lightgreen;
  }

  div.line {
    padding-left: 5px;
  }

  div.blah {
    text-align: left;
    width: 100%;
    /* padding: 0.2em; */
    border: 0px solid blue;
    margin: 0.15em 0;
  }
</style>
