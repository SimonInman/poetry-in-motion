<script lang="ts">
    import { Difficulty } from "./types.svelte";
    // let boxedWord: string;
    export let action: (word: string) => void;
    export let difficulty: Difficulty;
    // export let line_i: number;
    // export let word_j: number;
    export let word: string;
    let isHighlighted: boolean = false;
</script>

<button
    class="guessableWord"
    class:word={isHighlighted}
    on:mouseenter={() => {
        isHighlighted = true;
    }}
    on:mouseleave={() => {
        isHighlighted = false;
    }}
    on:click={() => action(word)}
>
    {#if difficulty === Difficulty.Medium && word.length > 2}
        {word[0]}----
    {:else}
        -----
    {/if}
</button>

<style>
    .guessableWord {
        border-color: white;
        background-color: white;
        display: inline-block;
        padding: 0px;
        border-width: 3px;
        border-style: solid;
        margin: 0;
    }
    .word {
        border-color: #ff3e00;
        border-style: solid;
    }
</style>
