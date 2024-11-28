<script>
  let { children } = $props();
</script>

<div class="w-[1024px] mx-auto mt-8 h-[576px] bg-slate-600 rounded">
  {@render children()}
</div>
