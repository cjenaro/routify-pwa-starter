<script>
  import { getConcestor, route } from '@sveltech/routify'
  import { fade } from 'svelte/transition'
  export let configs = []
  export let config = false
  const defaultConfig = {
    transition: fade,
    inParams: {},
    outParams: {},
  }
  $: oldRoute = $route.last || $route
  $: [concestor, ancestor, oldAncestor] = getConcestor($route.api, oldRoute.api)
  $: toAncestor = isAncestor(oldRoute, $route)
  $: toDescendant = isAncestor($route, oldRoute)
  $: toHigherIndex = ancestor && ancestor.meta.index > oldAncestor.meta.index
  $: toLowerIndex = ancestor && ancestor.meta.index < oldAncestor.meta.index
  $: meta = {
    toAncestor,
    toDescendant,
    toHigherIndex,
    toLowerIndex,
    routes: [$route, oldRoute],
    pages: [$route.api, oldRoute.api],
    ancestors: [ancestor, oldAncestor],
  }
  $: _config = configs.find(({ condition }) => condition(meta)) || config || defaultConfig
  $: normalizedConfig = { ...defaultConfig, ..._config }
  $: ({ transition, inParams, outParams } = normalizedConfig)
  
  function isAncestor(descendant, ancestor) {
    /* if(descendant.parent === ancestor.parent) return false */
    const { shortPath } = descendant.parent
    const { shortPath: shortPath2 } = ancestor.parent
    const descendantLength = descendant.filepath ? descendant.filepath.split('/').length : 0
    const ancestorLength = ancestor.filepath ? ancestor.filepath.split('/').length : 0
    return descendantLength > ancestorLength || descendantLength === ancestorLength && ancestor.isIndex
    /* return ancestor.isIndex && shortPath !== shortPath2 && shortPath.startsWith(shortPath2) */
  }
</script>

<style>
  .transition {
    position: absolute;
    height: 100%;
    width: 100%;
    left: 0;
    top: 0;
    padding: 8px;
    margin: 0;
    box-sizing: border-box;
  }
</style>

<div
  class="transition"
  in:transition|local={inParams}
  out:transition|local={outParams}
  >
  <slot />
</div>
