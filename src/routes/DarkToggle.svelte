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
  onclick={() => {
    document.getElementsByTagName("html")[0].classList.toggle("dark");
    isDark = !isDark;
  }}
>
  {#if isDark}<MoonSolid />{:else}<MoonOutline />{/if}
</button>
