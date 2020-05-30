<script>
  import { url } from "@sveltech/routify"
</script>

<style>
  h1 {
    text-align: center;
  }

  a {
    display: block;
    width: 100%;
    margin: 10px auto;
  }
</style>

<h1>Oops! No page was found!</h1>
<a href={$url()}>&larr; Go to home</a>
