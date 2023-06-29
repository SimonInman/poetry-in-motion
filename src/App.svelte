<script lang="ts">
  import GuessablePoem from "./GuessablePoem.svelte";
  import OrderablePoem from "./OrderablePoem.svelte";
  import type { Poem, RevealedWord } from "./types.svelte";
  import { Difficulty } from "./types.svelte";
  import { poemsList } from "./poems.svelte";

  let SelectedPoem: Poem;
  let SelectedDifficulty = Difficulty.Easy;

  function setPoem(poem: Poem, difficulty: Difficulty) {
    SelectedPoem = poem;
    SelectedDifficulty = difficulty;
  }

  function clearPoem() {
    SelectedPoem = undefined;
    SelectedDifficulty = undefined;
  }
</script>

{#if SelectedPoem === undefined}
  <main>
    <h1>Poetry</h1>
    <h2>Select poem to start</h2>
    <div>
      <ul>
        {#each poemsList as poem}
          <li>
            <i>{poem.title}</i> by {poem.author}:
            <a on:click={() => setPoem(poem, Difficulty.Easy)}>Easy</a>
            {" ~ "}
            <a on:click={() => setPoem(poem, Difficulty.Medium)}>Medium</a>
            {" ~ "}
            <a on:click={() => setPoem(poem, Difficulty.Hard)}>Hard</a>
          </li>
        {/each}
      </ul>
    </div>
  </main>
{:else}
  <main>
    <a style="float: left;" on:click={() => clearPoem()}>Back</a>
    <h1 style="display: inline-block">
      {SelectedPoem.title} BY {SelectedPoem.author}
    </h1>
    {#if SelectedDifficulty === Difficulty.Easy}
      <OrderablePoem poem={SelectedPoem} />
    {:else}
      <GuessablePoem poem={SelectedPoem} difficulty={SelectedDifficulty} />
    {/if}
  </main>
{/if}

<style>
  main {
    text-align: center;
    padding: 0.5em;
    max-width: 240px;
    margin: 0 auto;
    box-sizing: border-box;
  }

  *,
  *:before,
  *:after {
    box-sizing: inherit;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 2em;
    font-weight: 100;
  }

  li {
    margin: 15px 0;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
