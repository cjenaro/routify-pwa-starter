<script>
  import { url } from '@sveltech/routify'
</script>

<style>
  nav {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    flex-wrap: wrap;
  }

  nav a {
    width: 100%;
    text-align: center;
    line-height: 2;
    display: block;
    margin-bottom: 1rem;
    font-size: 1.3rem;
  }

  h1 {
    text-align: center;
  }
</style>

<h1>Click on the links to navigate!</h1>
<nav>
  <a href={$url("/page-1")}>Page 1 &rarr;</a>
  <a href={$url("/parameter")}>Page with parameter &rarr;</a>
  <a href={$url("/test/page")}>Nested path &rarr;</a>
</nav>
