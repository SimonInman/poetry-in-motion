<script lang="ts">
  import GuessablePoem from "./GuessablePoem.svelte";
  import OrderablePoem from "./OrderablePoem.svelte";
  import type { Poem, RevealedWord } from "./types.svelte";
  import { RoadNotTaken, DulceEt, Eagle, Sonnet116, Tide, poemsList} from "./poems.svelte";
  import poems from "./poems.svelte";

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

  function clearPoem() {
    SelectedPoem = undefined;
    SelectedDifficulty = undefined;
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
    {#each poemsList as poem}
        <li>
          <i>{poem.title}</i> by {poem.author}:
          <a on:click={() => setPoem(poem, Difficulty.Easy)}>Easy</a>
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
    <h1 style="display: inline-block">{SelectedPoem.title} BY {SelectedPoem.author}</h1>
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

  li{
    margin: 15px 0;
}

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
