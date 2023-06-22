<script lang="ts">
  import GuessablePoem from "./GuessablePoem.svelte";
  import OrderablePoem from "./OrderablePoem.svelte";
  import type { Poem, RevealedWord } from "./types.svelte";
  import { RoadNotTaken, DulceEt, Eagle } from "./poems.svelte";

  export let name: string;

  enum Difficulty {
    Easy = 1,
    Hard,
  }

  let SelectedPoem: Poem;
  let SelectedDifficulty = Difficulty.Easy;

  let word_set;
  let guessed_words = new Set<string>();

  function setPoem(poem: Poem, difficulty: Difficulty) {
    SelectedPoem = poem;
    SelectedDifficulty = difficulty;
  }

  function check_guess(guess: string) {
    if (word_set === undefined) {
      let poem_as_list = SelectedPoem.rawPoem
        .join(" ")
        .split(" ")
        .map((s) => s.replace(/[^A-Za-z0-9-]/g, ""))
        .map((w) => w.toUpperCase());
      word_set = new Set(poem_as_list);
    }

    let upper_guess = name.toUpperCase();
    if (word_set.has(upper_guess) && !guessed_words.has(upper_guess)) {
      guessed_words.add(upper_guess);
      guessed_words = guessed_words;
      name = "";
    }
  }
</script>

{#if SelectedPoem === undefined}
  <main>
    <h1>Poetry</h1>
    <h2>Select poem to start</h2>
    <div>
      <ul>
        <li>
          <i>The Road Not Taken</i> by Robert Frost:
          <a on:click={() => setPoem(RoadNotTaken, Difficulty.Easy)}>Easy</a>
          {" ~ "}
          <a on:click={() => setPoem(RoadNotTaken, Difficulty.Hard)}>Hard</a>
        </li>
        <li>
          <i>Dulce Et Decorum Est</i> by Wilfred Owen:
          <a on:click={() => setPoem(DulceEt, Difficulty.Easy)}>Easy</a>
          {" ~ "}
          <a on:click={() => setPoem(DulceEt, Difficulty.Hard)}>Hard</a>
        </li>
        <li>
          <i>The Eagle</i> by Alfred, Lord Tennyson:
          <a on:click={() => setPoem(Eagle, Difficulty.Easy)}>Easy</a>
          {" ~ "}
          <a on:click={() => setPoem(Eagle, Difficulty.Hard)}>Hard</a>
        </li>
      </ul>
    </div>
  </main>
{:else}
  <main>
    <h1>{SelectedPoem.title} BY {SelectedPoem.author}</h1>
    {#if SelectedDifficulty === Difficulty.Easy}
      <h3>Drag the poem lines into the correct order on the right-hand box</h3>

      <br />
      <OrderablePoem poem={SelectedPoem} />
    {:else}
      <input
        bind:value={name}
        on:input={() => check_guess(name)}
        placeholder="Enter poem words here..."
        size="100"
      />
      <br />
      <GuessablePoem poem={SelectedPoem} {guessed_words} />
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

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
