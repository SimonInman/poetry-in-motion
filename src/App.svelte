<script lang="ts">
  import GuessablePoem from "./GuessablePoem.svelte";
  import type { Poem, RevealedWord } from "./types.svelte";

  export let name: string;
  let poem = [
    "Bent double, like old beggars under sacks,",
    "Knock-kneed, coughing like hags, we cursed through sludge,",
    " Till on the haunting flares we turned our backs",
    "And towards our distant rest began to trudge.",
    "Men marched asleep. Many had lost their boots",
    "But limped on, blood-shod. All went lame; all blind;",
    "Drunk with fatigue; deaf even to the hoots",
    "Of gas-shells dropping softly behind.",
    "\n",
    "Gas! GAS! Quick, boys!—An ecstasy of fumbling",
    "Fitting the clumsy helmets just in time,",
    "But someone still was yelling out and stumbling",
    "And flound’ring like a man in fire or lime.—",
    "Dim through the misty panes and thick green light,",
    "As under a green sea, I saw him drowning.",
    "\n",
    "In all my dreams before my helpless sight,",
    "He plunges at me, guttering, choking, drowning.",
    "\n",
    "If in some smothering dreams, you too could pace",
    "Behind the wagon that we flung him in,",
    "And watch the white eyes writhing in his face,",
    "His hanging face, like a devil’s sick of sin;",
    "If you could hear, at every jolt, the blood",
    "Come gargling from the froth-corrupted lungs,",
    "Obscene as cancer, bitter as the cud",
    "Of vile, incurable sores on innocent tongues,—",
    "My friend, you would not tell with such high zest",
    "To children ardent for some desperate glory,",
    "The old Lie: Dulce et decorum est",
    "Pro patria mori.",
  ];

  //   let parsed_poem = poem.split(" ").map((s) => s.replace(/\W/g, ""));
  let poemStruct: Poem = { rawPoem: poem };
  let poem_as_list = poem
    .join(" ")
    .split(" ")
    .map((s) => s.replace(/[^A-Za-z0-9-]/g, ""))
    .map((w) => w.toUpperCase());
  let word_set = new Set(poem_as_list);
  let guessed_words = new Set<string>();
  //   let guessed_words = new Set<RevealedWord>();

  function check_guess(guess: string) {
    let upper_guess = name.toUpperCase();
    if (word_set.has(upper_guess) && !guessed_words.has(upper_guess)) {
      guessed_words.add(upper_guess);
      guessed_words = guessed_words;
      name = "";
    }
  }
</script>

<main>
  <h1>Dulce et decorum est By Wilfred Owen</h1>
  <input
    bind:value={name}
    on:input={() => check_guess(name)}
    placeholder="Enter poem words here..."
    size="100"
  />
  <br />
  <GuessablePoem poem={poemStruct} {guessed_words} />
</main>

<style>
  main {
    text-align: center;
    padding: 0.5em;
    max-width: 240px;
    margin: 0 auto;
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
