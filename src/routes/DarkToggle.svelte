<script>
  import MoonOutline from "$lib/icons/MoonOutline.svelte";
  import MoonSolid from "$lib/icons/MoonSolid.svelte";
  import { onMount } from "svelte";
  let isDark = $state(false);
  onMount(() => {
    isDark = document
      .getElementsByTagName("html")[0]
      .classList.contains("dark");
  });
</script>

<button
  class="hover:bg-slate-300 rounded-full p-1.5 pl-1 pb-1 dark:text-slate-100 dark:hover:bg-slate-500"
  onclick={() => {
    document.getElementsByTagName("html")[0].classList.toggle("dark");
    isDark = !isDark;
  }}
>
  {#if isDark}<MoonSolid />{:else}<MoonOutline />{/if}
</button>
