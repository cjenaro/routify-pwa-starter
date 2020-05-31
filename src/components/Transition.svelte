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
      condition: c => c.toDescendant || c.routes[1].path.includes('index'),
      transition: fly,
      inParams: { x: $width, duration: 500, opacity: 1 },
      outParams: { x: -$width, duration: 300, opacity: 1 },
    },
    {
      condition: c => c.toAncestor || c.routes[0].path.includes('index'),
      transition: fly,
      inParams: { x: -$width, duration: 500, opacity: 1 },
      outParams: { x: $width, duration: 300, opacity: 1 },
    },
    {
      // No matching config. We don't want a transition
      condition: (c) => {
        console.log(c)
        return true
      },
      transition: () => {},
    },
  ]
</script>

<ForkedBaseTransition {configs}>
  <slot />
</ForkedBaseTransition>
