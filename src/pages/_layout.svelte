<script>
  import { url } from "@sveltech/routify"
  import { writable } from 'svelte/store';
  import Transition from "../components/Transition.svelte"
  const width = writable();
</script>

<style>
  #layout {
    overflow-x: hidden;
    height: 100%;
    position: relative;
  }

  a {
    padding: 8px;
    display: block;
  }
</style>

<a href={$url("/")}>Home</a>
<div id="layout" bind:offsetWidth={$width}>
  <slot decorator={Transition} scoped={{ width }} />
</div>

