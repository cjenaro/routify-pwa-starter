<script>
  import { url } from "@sveltech/routify"
  import { writable } from 'svelte/store';
  import Transition from "../components/Transition.svelte"
  const width = writable();
</script>

<a href={$url("/")}>Home</a>
<div bind:offsetWidth={$width}>
  <slot decorator={Transition} scoped={{ width }} />
</div>

