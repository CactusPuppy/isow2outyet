<script lang="ts">
  import {formatDistanceToNowStrict, differenceInCalendarDays, format} from "date-fns";
  import { onDestroy, onMount } from "svelte";

  export let ow2ReleaseDate = new Date(2077, 4, 20);
  $: now = new Date(Date.now());
  $: isOW2Out = now > ow2ReleaseDate;
  let releaseDateAnnounced = false;

  export let nextOW2NewsDate = new Date(2022, 5, 16);

  let timeUpdater : NodeJS.Timer;
  onMount(() => {
    timeUpdater = setInterval(() => {
      now = new Date();
    }, 500);
  });

  onDestroy(() => {
    clearInterval(timeUpdater);
  });
</script>

<div class="flex flex-col justify-center items-center h-[100vh] w-[100vw]">
  <div class="flex-grow flex flex-col justify-center items-center py-8">
    <h1 class="text-7xl font-display font-semibold dark:text-slate-100">{isOW2Out ? "Yes." : "Not yet."}</h1>
    {#if !isOW2Out}
      <p class="mt-4 mx-2 text- italic dark:text-slate-100 text-center">
        ...but there {differenceInCalendarDays(now, ow2ReleaseDate) === 1 ? "is" : "are"}
        {#if releaseDateAnnounced}
          <span class="text-ow2-orange dark:text-ow2-light-orange">{differenceInCalendarDays(now, ow2ReleaseDate) >= 1 ? differenceInCalendarDays(now, ow2ReleaseDate) : formatDistanceToNowStrict(ow2ReleaseDate)} </span>
          until release on <span class="text-ow2-orange dark:text-ow2-light-orange">{format(ow2ReleaseDate, "MMMM do, yyyy")}</span>
        {:else if nextOW2NewsDate > now}
          <span class="text-ow2-orange dark:text-ow2-light-orange">{differenceInCalendarDays(now, nextOW2NewsDate) >= 1 ? differenceInCalendarDays(now, nextOW2NewsDate) : formatDistanceToNowStrict(nextOW2NewsDate)} </span>
          until more OW2 news on <span class="text-ow2-orange dark:text-ow2-light-orange">{format(nextOW2NewsDate, "MMMM do, yyyy")}</span>
        {/if}
      </p>
    {/if}
  </div>
  <div class="flex justify-between my-4 mx-2 px-4 h-8 w-full">
    <p class="text-xs text-gray-500 dark:text-slate-400 italic text-left">Created by <a class="text-ow2-orange dark:text-ow2-light-orange underline" href="https://twitter.com/Cactus_Puppy" rel="noreferrer noopener" target="_blank">@Cactus_Puppy</a><br /><a href="https://github.com/CactusPuppy/isow2outyet" rel="noreferrer noopener" target="_blank" class="text-ow2-orange dark:text-ow2-light-orange underline">GitHub</a></p>
    <p class="text-xs text-gray-500 dark:text-slate-400 italic text-right">
      This site and its creator are not affiliated with Overwatch or Blizzard Entertainment.
      <br />Overwatch 2 and the Overwatch 2 logo are ©2022 Blizzard Entertainment, Inc.
    </p>
  </div>
</div>
