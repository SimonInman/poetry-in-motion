<script lang="ts">
  import GuessablePoem from "./GuessablePoem.svelte";
  import OrderablePoem from "./OrderablePoem.svelte";
  import type { Poem, RevealedWord } from "./types.svelte";
  import { RoadNotTaken, DulceEt } from "./poems.svelte";

  export let name: string;

  enum Difficulty {
    Easy = 1,
    Hard,
  }

  let SelectedPoem: Poem;
  let SelectedDifficulty = Difficulty.Easy;

  // let poem = [
  //   "Two roads diverged in a yellow wood,",
  //   "And sorry I could not travel both",
  //   "And be one traveler, long I stood",
  //   "And looked down one as far as I could",
  //   "To where it bent in the undergrowth;",
  //   "\n",
  //   "Then took the other, as just as fair,",
  //   "And having perhaps the better claim,",
  //   "Because it was grassy and wanted wear;",
  //   "Though as for that the passing there",
  //   "Had worn them really about the same,",
  //   "\n",
  //   "And both that morning equally lay",
  //   "In leaves no step had trodden black.",
  //   "Oh, I kept the first for another day!",
  //   "Yet knowing how way leads on to way,",
  //   "I doubted if I should ever come back.",
  //   "\n",
  //   "I shall be telling this with a sigh",
  //   "Somewhere ages and ages hence:",
  //   "Two roads diverged in a wood, and I—",
  //   "I took the one less traveled by,",
  //   "And that has made all the difference.",
  // ];

  // let poem2 = [
  //   "Bent double, like old beggars under sacks,",
  //   "Knock-kneed, coughing like hags, we cursed through sludge,",
  //   " Till on the haunting flares we turned our backs",
  //   "And towards our distant rest began to trudge.",
  //   "Men marched asleep. Many had lost their boots",
  //   "But limped on, blood-shod. All went lame; all blind;",
  //   "Drunk with fatigue; deaf even to the hoots",
  //   "Of gas-shells dropping softly behind.",
  //   "\n",
  //   "Gas! GAS! Quick, boys!—An ecstasy of fumbling",
  //   "Fitting the clumsy helmets just in time,",
  //   "But someone still was yelling out and stumbling",
  //   "And flound’ring like a man in fire or lime.—",
  //   "Dim through the misty panes and thick green light,",
  //   "As under a green sea, I saw him drowning.",
  //   "\n",
  //   "In all my dreams before my helpless sight,",
  //   "He plunges at me, guttering, choking, drowning.",
  //   "\n",
  //   "If in some smothering dreams, you too could pace",
  //   "Behind the wagon that we flung him in,",
  //   "And watch the white eyes writhing in his face,",
  //   "His hanging face, like a devil’s sick of sin;",
  //   "If you could hear, at every jolt, the blood",
  //   "Come gargling from the froth-corrupted lungs,",
  //   "Obscene as cancer, bitter as the cud",
  //   "Of vile, incurable sores on innocent tongues,—",
  //   "My friend, you would not tell with such high zest",
  //   "To children ardent for some desperate glory,",
  //   "The old Lie: Dulce et decorum est",
  //   "Pro patria mori.",
  // ];

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
