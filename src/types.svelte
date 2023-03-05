<script context="module" lang="ts">
  import Poems from "./poems.svelte";


  export type Poem = {
    // The lines of the Poem.
    rawPoem: string[];
    title: string;
    author: string;
  };

  export type RevealedWord = {
    word: string;
    clicked: boolean;
  };
</script>
