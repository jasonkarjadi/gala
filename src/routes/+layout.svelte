<script>
  import "../app.css";
  import DarkToggle from "./DarkToggle.svelte";
  let { children } = $props();
</script>

<header class="flex h-14 px-12 justify-between items-center">
  <a
    href="/"
    class="font-bold inline-block text-xl content-center px-4 rounded-b h-full hover:bg-slate-300 active:bg-slate-400 dark:text-slate-100 dark:hover:bg-slate-600 dark:active:bg-slate-500"
  >
    GALA
  </a>
  <DarkToggle />
</header>
<main>
  {@render children()}
</main>
<footer class="text-center text-xs dark:text-slate-100">© GALA 2025</footer>
