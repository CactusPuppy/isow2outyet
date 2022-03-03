<script lang="ts">
  export let ow2ReleaseDate = new Date(2077, 4, 20);
  $: isOW2Out = new Date(Date.now()) > ow2ReleaseDate;
</script>

<div class="flex flex-col justify-center items-center h-[100vh] w-[100vw] bg-slate-100 dark:bg-slate-800">
  <div class="flex-grow flex flex-col justify-center items-center py-8">
    <h1 class="text-6xl font-display font-medium dark:text-slate-100">{isOW2Out ? "Yes." : "No."}</h1>
  </div>
  <div class="my-4 mx-2 h-8">
    <p class="text-xs text-gray-500 dark:text-slate-400 italic text-center">Created by <a class="text-blue-500 dark:text-blue-300 underline" href="https://twitter.com/Cactus_Puppy" rel="noreferrer noopener" target="_blank">@Cactus_Puppy</a></p>
    <p class="text-xs text-gray-500 dark:text-slate-400 italic text-center">Overwatch 2 and the Overwatch 2 logo are ©2022 Blizzard Entertainment, Inc.</p>
  </div>
</div>
