<script lang="ts">
  import type { Poem } from "./types.svelte";
  export let poem: Poem;
  export let guessed_words: Set<string>;
  let boxedWord: string;

  let poemLines = poem.rawPoem.map((line) => line_to_words(line));

  // let poem_as_list = poem.rawPoem
  //   .split(" ")
  //   .map((s) => s.replace(/[^A-Za-z0-9-]/g, ""));
  // .map((w) => toUpperCase());
  //   let word_set = new Set(poem_as_list);

  function line_to_words(line: string): string[] {
    return line.split(" ").map((s) => s.replace(/[^A-Za-z0-9-]/g, ""));
  }

  function reveal_word(word: string): any {
    let upper_guess = word.toUpperCase();
    guessed_words.add(upper_guess);
    guessed_words = guessed_words;
  }
</script>

<!-- <p>{poemLines}</p> -->
<div style="text-align: center;">
  <div class="poem">
    {#each poemLines as line, line_i}
      <!-- let line_as_list = poem.rawPoem .split(" ") .map((s) =>
  s.replace(/[^A-Za-z0-9-]/g, "")); -->
      {#if line.length == 1 && line[0] === ""}
        <br />
      {:else}
        {#each line as word, word_j}
          {#if guessed_words.has(word.toUpperCase())}
            {word}{" "}
          {:else}
            <span
              class:word={`${line_i}_${word_j}` === boxedWord}
              on:mouseenter={() => {
                boxedWord = `${line_i}_${word_j}`;
                console.log(boxedWord);
              }}
              on:mouseleave={() => {
                boxedWord = "";
              }}
              on:click={() => reveal_word(word)}
            >
              -----
            </span>
            {" "}
          {/if}
        {/each}
        <br />
      {/if}
    {/each}
  </div>
</div>
<p>guessed words: {guessed_words.size}</p>
<p>BANG</p>

<style>
  div.poem {
    text-align: left;
    display: inline-block;
    font-size: medium;
    /* line-height: 50%; */
    font-family: "Times New Roman", Times, serif;
  }

  span {
    border-color: white;
    border-style: solid;
    /* padding-top: 2px;
    padding-bottom: 2px; */
    display: inline-block;
  }

  .word {
    border-color: #ff3e00;
    border-style: solid;
  }
</style>
