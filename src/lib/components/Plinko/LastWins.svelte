<script lang="ts">
  import { binColorsByRowCount } from '$lib/constants/game';
  import { runningTotal, winRecords } from '$lib/stores/game';

  type Props = {
    /**
     * Number of last wins to display.
     */
    winCount?: number;
  };

  let { winCount = 4 }: Props = $props();

  let lastWins = $derived($winRecords.slice(-winCount).toReversed());
</script>

<div class="flex flex-col items-center gap-1">
  <div
    class="flex w-12 items-center justify-center rounded-md bg-acm-card py-1 text-sm font-bold tabular-nums"
    class:text-green-400={$runningTotal >= 0}
    class:text-red-400={$runningTotal < 0}
  >
    {$runningTotal}
  </div>
  <div
    class="flex w-[clamp(1.5rem,0.893rem+2.857vw,2rem)] flex-col overflow-hidden rounded-xs text-[clamp(8px,5.568px+0.714vw,10px)] md:rounded-md lg:w-12 lg:text-sm"
    style:aspect-ratio={`1 / ${winCount}`}
  >
    {#each lastWins as { binIndex, rowCount, payout: { multiplier } }}
      <div
        class="flex aspect-square items-center justify-center font-bold text-gray-950"
        style:background-color={binColorsByRowCount[rowCount].background[binIndex]}
      >
        {multiplier}
      </div>
    {/each}
  </div>
</div>
