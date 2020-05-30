<script>
  import { url } from "@sveltech/routify"
  export let parameter
</script>

<h1>This page has the parameter: {parameter}</h1>
<a href={$url("/")}>&larr; Go back to home</a>
