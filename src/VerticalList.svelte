<script>
  import { flip } from "svelte/animate";
  import { dndzone } from "svelte-dnd-action";
  export let items;

  //   let correctlyPlacedSet: Set<number>;
  let correctlyPlacedSet = new Set();

  const flipDurationMs = 300;

  function handleDndConsider(e) {
    items = e.detail.items;
  }

  function handleDndFinalize(e) {
    let ItemsWithIndex = e.detail.items.map((item, currentIndex) => {
      return { currentIndex: currentIndex, item: item };
    });
    let correctlyPlacedItems = ItemsWithIndex.filter((itemWithIndex) => {
      return itemWithIndex.currentIndex == itemWithIndex.item.id;
    }).map((itemWithIndex) => itemWithIndex.currentIndex);
    correctlyPlacedSet = new Set(correctlyPlacedItems);
    console.log(correctlyPlacedSet);
    console.log(correctlyPlacedSet.has(0));
    items = e.detail.items;
  }
</script>

<section
  use:dndzone={{ items, flipDurationMs }}
  on:consider={handleDndConsider}
  on:finalize={handleDndFinalize}
>
  {#each items as item (item.id)}
    <div class="blah" animate:flip={{ duration: flipDurationMs }}>
      <div class="line" class:correct={correctlyPlacedSet.has(item.id)}>
        {#if item.name === "\n"}
          {" _ "}
        {:else}
          {item.name}
        {/if}
      </div>
    </div>
  {/each}
</section>

<style>
  section {
    width: 100%;
    padding: 0.3em;
    border: 1px solid black;
    overflow: scroll;
    height: 1620px;
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
    border: 1px solid blue;
    margin: 0.15em 0;
  }
</style>
