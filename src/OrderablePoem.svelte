<script lang="ts">
  //   import { dndzone } from "svelte-dnd-action";
  import VerticalList from "./VerticalList.svelte";

  import type { Poem } from "./types.svelte";
  import LineBank from "./LineBank.svelte";
  import LineSlot from "./LineSlot.svelte";
  export let poem: Poem;
  //   export let guessed_words: Set<string>;
  let MockItems = [
    { id: 0, name: "Bent double, like old beggars under sacks," },
    {
      id: 1,
      name: "Knock-kneed, coughing like hags, we cursed through sludge,",
    },
  ];

  let poem_as_list_with_index = poem.rawPoem.map((line, index) => {
    return { id: index, name: line };
  });
  let ShuffledWithIndexes = poem_as_list_with_index
    .map((value) => ({ value, sort: Math.random() }))
    .sort((a, b) => a.sort - b.sort)
    .map(({ value }) => value);

  //   console.log(shuffled);
  //   .split(" ")
  //   .map((s) => s.replace(/[^A-Za-z0-9-]/g, ""));
  // .map((w) => toUpperCase());
  //   let word_set = new Set(poem_as_list);
  //   console.log(poem_as_list_with_index);
</script>

<!-- <VerticalList items={MockItems} /> -->
<div class="container">
  <div class="flex-item">
    <LineBank items={ShuffledWithIndexes} />
  </div>
  <div class="spacer" />

  <div class="flex-item">
    <!-- <VerticalList items={[]} /> -->
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

<!-- <VerticalList items={poem_as_list_with_index} /> -->
<style>
  .container {
    /* background-color: #2e4272; */
    display: flex;
    width: 100%;
  }
  .flex-item {
    /* flex-grow: 1; */
    width: 50%;
  }
  div.spacer {
    font-size: 0;
    width: 20px;
    line-height: 0;
  }
  div.spacer {
    font-size: 0;
    height: 10px;
    line-height: 0;
  }
</style>
