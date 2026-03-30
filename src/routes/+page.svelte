<script lang="ts">
  import LiveStatsWindow from '$lib/components/LiveStatsWindow/LiveStatsWindow.svelte';
  import Plinko from '$lib/components/Plinko';
  import SettingsWindow from '$lib/components/SettingsWindow';
  import Sidebar from '$lib/components/Sidebar';
  import { setBalanceFromLocalStorage, writeBalanceToLocalStorage } from '$lib/utils/game';
  import GitHubLogo from 'phosphor-svelte/lib/GithubLogo';

  $effect(() => {
    setBalanceFromLocalStorage();
  });
</script>

<svelte:window onbeforeunload={writeBalanceToLocalStorage} />

<div class="flex h-dvh w-full flex-col overflow-hidden">
  <nav class="z-10 w-full border-b border-acm-border bg-acm-bg px-5">
    <div class="mx-auto flex h-14 max-w-6xl items-center gap-3">
      <img src="/acm-logo.png" alt="ACM" class="h-7" />
      <span class="bg-gradient-to-r from-[#FFB800] to-[#ADFF00] bg-clip-text text-2xl font-semibold text-transparent">ACM Plinko</span>
    </div>
  </nav>

  <div class="flex min-h-0 flex-1 px-5 py-3">
    <div class="mx-auto flex w-full max-w-7xl min-w-[300px]">
      <div class="flex min-h-0 w-full overflow-hidden rounded-xl border border-acm-border lg:flex-row">
        <Sidebar />
        <div class="min-h-0 flex-1">
          <Plinko />
        </div>
      </div>
    </div>
  </div>

  <SettingsWindow />
  <LiveStatsWindow />

  <footer class="px-5 py-2">
    <div class="mx-auto flex max-w-6xl items-center justify-between">
      <p class="text-xs text-acm-muted">
        ACM UTD © {new Date().getFullYear()}
      </p>
      <a
        href="https://github.com/acmutd/acm-plinko"
        target="_blank"
        rel="noreferrer"
        class="flex items-center gap-1 p-1 text-xs text-acm-muted transition hover:text-white"
      >
        <GitHubLogo class="size-4" weight="bold" />
        <span>built w/ ♡ by acm dev</span>
      </a>
    </div>
  </footer>
</div>

<style lang="postcss">
  @reference "../app.css";

  :global(body) {
    @apply bg-acm-bg;
  }
</style>
