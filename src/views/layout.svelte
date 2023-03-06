<script>
  import { Route } from "svelte-router-spa";
  //   import TopHeader from "./top_header.svelte";
  export let currentRoute;
  const params = {};
</script>

<div class="app">
  <!-- <TopHeader /> -->
  <h1>hello</h1>
  <section class="section">
    <Route {currentRoute} {params} />
  </section>
</div>
