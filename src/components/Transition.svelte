<script>
  import { fly } from 'svelte/transition'
  import { linear } from 'svelte/easing'
  import ForkedBaseTransition from "./ForkedBaseTransition.svelte"

  export let scoped
  const { width } = scoped
  const configs = [
    {
      condition: ({ routes }) => routes[0] === routes[1],
      transition: () => {},
    },
    {
      condition: c => c.toDescendant,
      transition: fly,
      inParams: { x: $width, duration: 500, opacity: 1 },
      outParams: { x: -$width - 100, duration: 400, opacity: 1 },
    },
    {
      condition: c => c.toAncestor,
      transition: fly,
      inParams: { x: -$width, duration: 500, opacity: 1 },
      outParams: { x: $width + 100, duration: 400, opacity: 1 },
    },
    {
      // No matching config. We don't want a transition
      condition: (c) => true,
      transition: () => {},
    },
  ]
</script>

<ForkedBaseTransition {configs}>
  <slot />
</ForkedBaseTransition>
