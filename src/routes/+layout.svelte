<script>
  import "../app.css";
  import DarkToggle from "./DarkToggle.svelte";
  let { children } = $props();
</script>

<header class="flex h-16 px-12 justify-between">
  <a
    href="/"
    class="font-bold inline-block text-xl content-center px-4 hover:bg-slate-300 active:bg-slate-400 dark:text-slate-100 dark:hover:bg-slate-600 dark:active:bg-slate-500"
  >
    GALA
  </a>
  <DarkToggle />
</header>
{@render children()}
<footer class="text-center text-xs">© GALA 2025</footer>
