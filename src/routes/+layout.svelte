<script lang="ts">
  import type { Snippet } from 'svelte';
  import '../app.css';

  let { children }: { children: Snippet } = $props();
</script>

<svelte:head>
  <title>ACM Plinko</title>
  <link rel="icon" href="/favicon.ico" />
  <meta property="og:type" content="website" />
  <meta property="og:title" content="ACM Plinko" />
</svelte:head>

{@render children?.()}
