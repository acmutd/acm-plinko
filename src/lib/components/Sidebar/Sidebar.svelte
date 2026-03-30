<script lang="ts">
  import { plinkoEngine, runningTotal, totalProfitHistory, winRecords } from '$lib/stores/game';
  import { isLiveStatsOpen } from '$lib/stores/layout';
  import { flyAndScale } from '$lib/utils/transitions';
  import { Tooltip } from 'bits-ui';
  import ChartLine from 'phosphor-svelte/lib/ChartLine';
  import { twMerge } from 'tailwind-merge';

  let isDropBallDisabled = $derived($plinkoEngine === null);
</script>

<div class="flex flex-col gap-5 bg-acm-card p-3 lg:w-64 lg:shrink-0">
  <button
    onclick={() => $plinkoEngine?.dropBall()}
    disabled={isDropBallDisabled}
    class="touch-manipulation rounded-md bg-gradient-to-r from-[#FFB800] to-[#ADFF00] py-3 font-semibold text-gray-950 transition-opacity hover:opacity-90 active:opacity-80 disabled:opacity-40"
  >
    Drop Ball
  </button>

  <button
    onclick={() => { $runningTotal = 0; $winRecords = []; $totalProfitHistory = [0]; }}
    class="touch-manipulation rounded-md border border-acm-border py-2 text-sm font-medium text-acm-muted transition hover:border-[hsl(0_0%_20%)] hover:text-white active:bg-[hsl(0_0%_14.9%)]"
  >
    Reset
  </button>

  <div class="mt-auto pt-5">
    <div class="flex items-center justify-center border-t border-acm-border pt-3">
      <Tooltip.Provider delayDuration={0} disableCloseOnTriggerClick>
        <!-- Live Stats Button -->
        <Tooltip.Root>
          <Tooltip.Trigger
            onclick={() => ($isLiveStatsOpen = !$isLiveStatsOpen)}
            class={twMerge(
              'rounded-full p-2 text-acm-muted transition hover:bg-[hsl(0_0%_14.9%)] active:bg-[hsl(0_0%_20%)]',
              $isLiveStatsOpen && 'text-white',
            )}
          >
            <ChartLine class="size-6" weight="bold" />
          </Tooltip.Trigger>
          <Tooltip.Content
            forceMount
            sideOffset={4}
            class="z-30 max-w-lg rounded-md bg-white p-3 text-sm font-medium text-gray-950 drop-shadow-xl"
          >
            {#snippet child({ wrapperProps, props, open })}
              {#if open}
                <div {...wrapperProps}>
                  <div {...props} transition:flyAndScale>
                    <Tooltip.Arrow class="text-white" />
                    <p>{$isLiveStatsOpen ? 'Close' : 'Open'} Live Stats</p>
                  </div>
                </div>
              {/if}
            {/snippet}
          </Tooltip.Content>
        </Tooltip.Root>
      </Tooltip.Provider>
    </div>
  </div>
</div>
