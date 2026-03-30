<script lang="ts">
  import { runningTotal, winRecords } from '$lib/stores/game';
  import { twMerge } from 'tailwind-merge';

  let totalDrops = $derived($winRecords.length);
  let positiveHits = $derived($winRecords.filter(({ payout: { multiplier } }) => multiplier > 0).length);
  let negativeHits = $derived($winRecords.filter(({ payout: { multiplier } }) => multiplier < 0).length);
</script>

<div class="flex rounded-md bg-acm-bg p-4 text-sm">
  <div class="flex-1">
    <p class="font-medium text-acm-muted">Score</p>
    <p
      class={twMerge('font-semibold tabular-nums', $runningTotal >= 0 ? 'text-green-400' : 'text-red-400')}
    >
      {$runningTotal}
    </p>
  </div>
  <div class="mx-4 w-0.5 bg-acm-border" aria-hidden="true"></div>
  <div class="flex-1 space-y-2">
    <div>
      <p class="font-medium text-acm-muted">Drops</p>
      <p class="font-semibold text-white tabular-nums">{totalDrops}</p>
    </div>
    <div class="flex gap-4">
      <div>
        <p class="font-medium text-acm-muted">+</p>
        <p class="font-semibold text-green-400 tabular-nums">{positiveHits}</p>
      </div>
      <div>
        <p class="font-medium text-acm-muted">-</p>
        <p class="font-semibold text-red-400 tabular-nums">{negativeHits}</p>
      </div>
    </div>
  </div>
</div>
