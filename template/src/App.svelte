<script lang="ts">
  import { onMount } from "svelte";
  import { Router, Route } from "svelte-routing";
  import Slideshow from "./components/Slideshow.svelte";

  export let url: string = "";
</script>

<Router {url}>
  <Route path=":filename" let:params>
    <Slideshow
      sourceUrl={`/md/${params.filename}.md`}
      filename={params.filename} />
  </Route>
</Router>
