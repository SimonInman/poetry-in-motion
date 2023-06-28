<script context="module" lang="ts">
  import App from "./App.svelte";
  import type { Poem, RevealedWord } from "./types.svelte";

  export let Eagle: Poem = {
    title: "The Eagle",
    author: "Alfred, Lord Tennyson",
    rawPoem: [
      "He clasps the crag with crooked hands;",
      "Close to the sun in lonely lands,",
      "Ring'd with the azure world, he stands.",
      "\n",
      "The wrinkled sea beneath him crawls;",
      "He watches from his mountain walls,",
      "And like a thunderbolt he falls.",
    ],
  };

  export let Sonnet116: Poem = {
    title: "Sonnet 116",
    author: "William Shakespeare",
    rawPoem: [
      "Let me not to the marriage of true minds",
      "Admit impediments. Love is not love",
      "Which alters when it alteration finds,",
      "Or bends with the remover to remove.",
      "O no! it is an ever-fixed mark",
      "That looks on tempests and is never shaken;",
      "It is the star to every wand'ring bark,",
      "Whose worth's unknown, although his height be taken.",
      "Love's not Time's fool, though rosy lips and cheeks",
      "Within his bending sickle's compass come;",
      "Love alters not with his brief hours and weeks,",
      "But bears it out even to the edge of doom.",
      "If this be error and upon me prov'd,",
      "I never writ, nor no man ever lov'd.",
    ],
  };

  export let Tide: Poem = {
    title: "There is a tide in the affairs of men",
    author: "William Shakespeare",
    rawPoem: [
      "There is a tide in the affairs of men",
      "Which, taken at the flood, leads on to fortune;",
      "Omitted, all the voyage of their life",
      "Is bound in shallows and in miseries.",
      "On such a full sea are we now afloat;",
      "And we must take the current when it serves,",
      "Or lose our ventures.",
    ],
  };

  export let RoadNotTaken: Poem = {
    title: "The road not taken",
    author: "Robert Frost",
    rawPoem: [
      "Two roads diverged in a yellow wood,",
      "And sorry I could not travel both",
      "And be one traveler, long I stood",
      "And looked down one as far as I could",
      "To where it bent in the undergrowth;",
      "\n",
      "Then took the other, as just as fair,",
      "And having perhaps the better claim,",
      "Because it was grassy and wanted wear;",
      "Though as for that the passing there",
      "Had worn them really about the same,",
      "\n",
      "And both that morning equally lay",
      "In leaves no step had trodden black.",
      "Oh, I kept the first for another day!",
      "Yet knowing how way leads on to way,",
      "I doubted if I should ever come back.",
      "\n",
      "I shall be telling this with a sigh",
      "Somewhere ages and ages hence:",
      "Two roads diverged in a wood, and I—",
      "I took the one less traveled by,",
      "And that has made all the difference.",
    ],
  };

  export let DulceEt: Poem = {
    title: "Dulce Et Decorum Est",
    author: "Wilfred Owen",
    rawPoem: [
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
    ],
  };

  export let poemsList: Array<Poem> = [DulceEt, RoadNotTaken, Eagle, Sonnet116, Tide];
</script>
