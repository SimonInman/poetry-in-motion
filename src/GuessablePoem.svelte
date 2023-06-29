<script lang="ts">
  import GuessableWord from "./GuessableWord.svelte";
  import type { Poem, Difficulty } from "./types.svelte";
  export let poem: Poem;
  export let guessed_words: Set<string>;
  export let difficulty: Difficulty;
  let boxedWord: string;

  let poemLines = poem.rawPoem.map((line) => line_to_words(line));
  let cheated_words = new Set<string>();

  function line_to_words(line: string): string[] {
    return line.split(" ").map((s) => s.replace(/[^A-Za-z0-9-]/g, ""));
  }

  function cheat_word(word: string): any {
    let upper_guess = word.toUpperCase();
    cheated_words.add(upper_guess);
    cheated_words = cheated_words;
  }

  function reveal_word(word: string): any {
    let upper_guess = word.toUpperCase();
    guessed_words.add(upper_guess);
    guessed_words = guessed_words;
  }
</script>

<div style="text-align: center;">
  <div class="poem">
    {#each poemLines as line}
      {#if line.length == 1 && line[0] === ""}
        <br />
      {:else}
        {#each line as word}
          {#if cheated_words.has(word.toUpperCase())}
            <div class="cheated_word">{word}{" "}</div>
            {" "}
          {:else if guessed_words.has(word.toUpperCase())}
            {word}{" "}
          {:else}
            <GuessableWord {word} action={cheat_word} {difficulty} />
            {" "}
          {/if}
        {/each}
        <br />
      {/if}
    {/each}
  </div>
</div>
<p>guessed words: {guessed_words.size}</p>

<style>
  div.cheated_word {
    color: red;
    display: inline-block;
  }

  div.poem {
    text-align: left;
    display: inline-block;
    font-size: medium;
    font-family: "Times New Roman", Times, serif;
  }
</style>
