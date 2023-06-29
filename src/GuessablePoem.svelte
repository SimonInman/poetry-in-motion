<script lang="ts">
  import GuessableWord from "./GuessableWord.svelte";
  import type { Poem } from "./types.svelte";
  export let poem: Poem;
  export let guessed_words: Set<string>;
  let boxedWord: string;

  let poemLines = poem.rawPoem.map((line) => line_to_words(line));

  function line_to_words(line: string): string[] {
    return line.split(" ").map((s) => s.replace(/[^A-Za-z0-9-]/g, ""));
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
          {#if guessed_words.has(word.toUpperCase())}
            {word}{" "}
          {:else}
            <GuessableWord {word} action={reveal_word} />
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
  div.poem {
    text-align: left;
    display: inline-block;
    font-size: medium;
    font-family: "Times New Roman", Times, serif;
  }
</style>
