<script lang="ts">
  import VerticalList from "./VerticalList.svelte";

  import type { Poem } from "./types.svelte";
  import LineBank from "./LineBank.svelte";
  import LineSlot from "./LineSlot.svelte";
  export let poem: Poem;

  let poem_as_list_with_index = poem.rawPoem.map((line, index) => {
    return { id: index, name: line };
  });
  let ShuffledWithIndexes = poem_as_list_with_index
    .map((value) => ({ value, sort: Math.random() }))
    .sort((a, b) => a.sort - b.sort)
    .map(({ value }) => value);
</script>

<h3>Drag the poem lines into the correct order on the right-hand box</h3>

<br />
<div class="container">
  <div class="flex-item">
    <LineBank items={ShuffledWithIndexes} />
  </div>

  <div class="flex-item">
    <!-- Just need to hand each LineSlot a 0-N index.
    Use #each with the indexes as a little hack to do
    this. Also allows us to put the blank line spacers
    in with correct indexing -->
    {#each poem_as_list_with_index as poem}
      {#if poem.name === "\n"}
        <div class="vertical-spacer" />
      {:else}
        <LineSlot slotIndex={poem.id} items={[]} />
      {/if}
    {/each}
  </div>
</div>

<style>
  .container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    column-gap: 20px;
    width: 1000px;
    margin: 0 auto;
    box-sizing: border-box;
  }
  div.vertical-spacer {
    font-size: 0;
    border-bottom: 1px solid black;
    height: 24px;
    line-height: 0;
  }
</style>
