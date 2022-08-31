<script lang="ts">
  import {formatDistanceToNowStrict, differenceInCalendarDays, format, parseISO} from "date-fns";
  import { onDestroy, onMount } from "svelte";

  export let ow2ReleaseDate = parseISO("2022-10-04T11:00:00-7:00")
  $: now = new Date(Date.now());
  $: isOW2Out = now > ow2ReleaseDate;
  let releaseDateAnnounced = true;

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
    {#if (releaseDateAnnounced && now < ow2ReleaseDate)}
      <p class="mt-4 mx-2 text- italic dark:text-slate-100 text-center">
        ...but there {differenceInCalendarDays(now, ow2ReleaseDate) === 1 ? "is" : "are"}
        {#if releaseDateAnnounced && now < ow2ReleaseDate}
          <span class="text-ow2-orange dark:text-ow2-light-orange">{differenceInCalendarDays(ow2ReleaseDate, now) >= 1 ? `${differenceInCalendarDays(ow2ReleaseDate, now)} days` : formatDistanceToNowStrict(ow2ReleaseDate)} </span>
          until release on <span class="text-ow2-orange dark:text-ow2-light-orange">{format(ow2ReleaseDate, "MMMM do, yyyy")}</span>
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
